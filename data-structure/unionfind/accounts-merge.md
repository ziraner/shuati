Given a list`accounts`, each element`accounts[i]`is a list of strings, where the first element`accounts[i][0]`is aname, and the rest of the elements areemailsrepresenting emails of the account.

Now, we would like to merge these accounts. Two accounts definitely belong to the same person if there is some email that is common to both accounts. Note that even if two accounts have the same name, they may belong to different people as people could have the same name. A person can have any number of accounts initially, but all of their accounts definitely have the same name.

After merging the accounts, return the accounts in the following format: the first element of each account is the name, and the rest of the elements are emails**in sorted order**. The accounts themselves can be returned in any order.

**Example 1:**

```
Input:

accounts = [["John", "johnsmith@mail.com", "john00@mail.com"], ["John", "johnnybravo@mail.com"], ["John", "johnsmith@mail.com", "john_newyork@mail.com"], ["Mary", "mary@mail.com"]]

Output:
 [["John", 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com'],  ["John", "johnnybravo@mail.com"], ["Mary", "mary@mail.com"]]

Explanation:

The first and third John's are the same person as they have the common email "johnsmith@mail.com".
The second John and Mary are different people as none of their email addresses are used by other accounts.
We could return these lists in any order, for example the answer [['Mary', 'mary@mail.com'], ['John', 'johnnybravo@mail.com'], 
['John', 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com']] would still be accepted.
```

**Note:**

The length of `accounts`will be in the range`[1, 1000]`.

The length of`accounts[i]`will be in the range`[1, 10]`.

The length of`accounts[i][j]`will be in the range`[1, 30]`.

这个题考察unionfind因为用BFS的话有点复杂，用unionfind则比较容易。其实就是一道输出以大哥为单位的所有connected component题目。跟find weak connected component和connected component很类似，分为4步。

```
class Solution(object):
    def accountsMerge(self, accounts):
        """
        :type accounts: List[List[str]]
        :rtype: List[List[str]]
        """
        user_map, n = {}, len(accounts)
        for account in accounts:
            for email in account[1:]:
                if email not in user_map:
                    user_map[email] = account[0]
        uf = UnionFind(user_map)
        for account in accounts:
            email1 = account[1]
            for email2 in account[2:]:
                uf.union(email1, email2)
        father_map = {}
        for account in accounts:
            for email in account[1:]:
                father = uf.find(email)
                if father not in father_map:
                    father_map[father] = set([email])
                else:
                    father_map[father].add(email)
        ans = []
        for key in father_map.keys():
            user = user_map[key]
            emails = sorted(list(father_map[key]))
            vals = [user] + emails
            ans.append(vals[:])
        return ans
class UnionFind:
    def __init__(self, hashmap):
        self.father = {}
        for key in hashmap.keys():
            self.father[key] = key
    def find(self, a):
        if self.father[a] == a:
            return a
        self.father[a] = self.find(self.father[a])
        return self.father[a]
    def union(self, a, b):
        root_a = self.find(a)
        root_b = self.find(b)
        if root_a != root_b:
            self.father[root_a] = root_b
```




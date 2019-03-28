AlphaBet Sort

面经题目：有一个字母表，里面有其他星球的语言的字母先后顺序排序，然后有一串单词，请根据给出的字母排序sort这些单词。

思路1：用一个hashmap记住这些字母的先后顺序，用idx即可。然后在python中写自己的比较函数，然后去用sort函数调用自己写的比较函数

```
class Solution:
	def alphabetSort(self, alphabet, words):
		def word_comparator(word1, word2):
			l1, l2 = len(word1), len(word2)
			i, j = 0, 0
			while i < l1 and j < l2:
				if hm[word1[i]] < hm[word2[j]]:
					return -1
				if hm[word1[i]] > hm[word2[j]]:
					return 1
				i += 1
				j += 1
			if i < l1:
				return 1
			if j < l2:
				return -1
			return 0
		hm = {}
		for i, c in enumerate(alphabet):
			hm[c] = i
		words.sort(cmp = word_comparator)
		return words
sl = Solution()
print sl.alphabetSort2('cdfag', ['df','ag','cg'])
```

如果不允许用python中的sort函数可以需要自己写sort函数，用mergesort：

```
class Solution:
    	def alphabetSort2(self, alphabet, words):
		self.hm = {}
		for i, c in enumerate(alphabet):
			self.hm[c] = i
		self.sort(words)
		return words
	def sort(self, A):
		if not A:
			return A
		tmp = ['' for _ in xrange(len(A))]
		self.mergeSort(A, tmp, 0, len(A) - 1)
		return A
	def mergeSort(self, A, tmp, start, end):
		if start >= end:
			return
		mid = (start + end) / 2
		self.mergeSort(A, tmp, start, mid)
		self.mergeSort(A, tmp, mid + 1, end)
		self.merge(A, tmp, start, end)
	def merge(self, A, tmp, start, end):
		mid = (start + end) / 2
		left, right, index = start, mid + 1, start
		while left <= mid and right <= end:
			if self.isSmaller(A[left], A[right]):
				tmp[index] = A[left]
				left += 1
			else:
				tmp[index] = A[right]
				right += 1
			index += 1
		while left <= mid:
			tmp[index] = A[left]
			index += 1
			left += 1
		while right <= end:
			tmp[index] = A[right]
			index += 1
			right += 1
		for i in xrange(start, end + 1):
			A[i] = tmp[i]
	def isSmaller(self, word1, word2):
		l1, l2 = len(word1), len(word2)
		i, j = 0, 0
		while i < l1 and j < l2:
			if self.hm[word1[i]] < self.hm[word2[j]]:
				return True
			if self.hm[word1[i]] > self.hm[word2[j]]:
				return False
			i += 1
			j += 1
		if i < l1:
			return False
		return True
sl = Solution()
print sl.alphabetSort2('cdfag', ['df','ag','cg'])
```




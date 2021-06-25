1. 用Compartor进行排序写成functional模式s
```java
List<T> arrList = new ArrayList<>();
arrList.sort(Comparator.comparing((T t) -> t.someFunction).thenComparing((T t) -> t.someOtherFunction));
```

2. int[] arr -> arr.length
List<Integer> arrList -> arrList.size()

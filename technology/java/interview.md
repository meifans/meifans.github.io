

## 集合

### Array.sort与Collections.sort

    Arrays.sort(T[], Comparator < ? super T > c)

    Collections.sort(List<T> list,comparator<? super T> c)


**关系**

public static <T> void sort(List<T> list, Comparator<? super T> c) {
    list.sort(c);
}

Collections.sort --> list.sort() --> Arrays.sort()。
> ArrayList实现了sort，LinkedList使用了List接口default sort 方法，因为转换成对象数组的过程不同
> --> this.toArray() link是这样转成数组。

**模式**

Comparator 运用了策略模式,使不同的算法在运行时得以选择。通过传递不同的Comparator，可以选择对象不同的比较算法。

**策略**

数量<32 : 使用折半插入排序（binary insertion sort)，最适用于少量数据时，如果前面部分已经排序，可以排除掉，从无序的地方开始。
> 如果是init序列是递减的，会反转成递增的。

数量>=32 : 使用TimSort算法，就是找到已经排好序数据的子序列，然后对剩余部分排序，然后合并起来。
> 多次调用折半插入排序，排序其余的部分。

> ` Timsort是结合了合并排序（merge sort）和插入排序（insertion sort）而得出的排序算法，利用了数组原始的顺序，它在现实中有很好的效率。`

**泛型**

Comparator<? super T>  这样子类可以共用超类的Comparator方法。

**对象与基本类型**
Array.sort
  + 对象: 使用Timsort
  + 基本类型:  DualPivotQuicksort.sort
  > 改进的快速排序，采用多路快速排序，比单路快排有更好的性能。

---
title: 排序算法总结
date: 2020-09-01 00:36:38
categories: [算法]
tags: [算法,排序]
---

总结十大经典排序算法，分析稳定性、时间复杂度等内容；

### 算法相关定义

- 时间复杂度：

  在 大O符号表示法中，时间复杂度的公式是： T(n) = O( f(n) )，其中f(n) 表示每行代码执行次数之和，而 O 表示正比例关系，这个公式的全称是：**算法的渐进时间复杂度**。

  常见的时间复杂度量级有：

  <!--more-->

  - 常数阶O(1)

  <!--添加时间复杂度的详细计算方法-->

  - 对数阶O(logN)
  - 线性阶O(n)
  - 线性对数阶O(nlogN)
  - 平方阶O(n²)
  - 立方阶O(n³)
  - K次方阶O(n^k)
  - 指数阶(2^n)

- 空间复杂度：

  既然时间复杂度不是用来计算程序具体耗时的，那么也应该明白，空间复杂度也不是用来计算程序实际占用的空间的。空间复杂度是对一个算法在运行过程中临时占用存储空间大小的一个量度，同样反映的是一个趋势，用 S(n) 来定义。

  空间复杂度比较常用的有：O(1)、O(n)、O(n²)

- 内排序和外排序

  根据排序元素所在位置的不同,排序分: 内排序和外排序。

  - 内排序：指在排序期间数据对象全部存放在内存的排序。

  - 外排序：指在排序期间全部对象太多，不能同时存放在内存中，必须根据排序过程的要求，不断在内，外存间移动的排序。

  内排序在排序过程中，所有元素调到内存中进行的排序，内排序是排序的基础。内排序效率用比较次数来衡量。按所用策略不同，内排序又可分为插入排序、选择排序、交换排序、归并排序及基数排序等几大类。在数据量大的情况下，只能分块排序，但块与块间不能保证有序。外排序用读/写外存的次数来衡量其效率。

- 排序算法的稳定性

    假定在待排序的记录序列中，存在多个具有相同的关键字的记录，若经过排序，这些记录的相对次序保持不变，即在原序列中，**r<sub>i</sub>=r<sub>j</sub>**，且**r<sub>i</sub>**在**r<sub>j</sub>**之前，而在排序后的序列中，**r<sub>i</sub>**仍在**r<sub>j</sub>**之前，则称这种排序算法是稳定的；否则称为不稳定的。

### 十大经典排序算法对比

![](http://images.wpt6.cn/blog/2020-09-01-00-39-16.jpg)

### 代码

#### 冒泡排序

- 时间复杂度：O(n<sup>2</sup>)
- 空间复杂度：O(1)
- 稳定性：稳定
- 内排序：Y

##### 代码实现

```java
    public static void bubble(int[] array) {
        for (int i = 0; i < array.length; i++) {
            boolean isSorted = true;
            for (int j = 1; j < array.length-i; j++) {
                if(array[j]<array[j-1]){
                    int temp = array[j];
                    array[j] = array[j-1];
                    array[j-1]= temp;
                    isSorted = false;
                }
            }
            if (isSorted) {
                break;
            }
        }
    }
```

#### 选择排序


- 时间复杂度：O(n<sup>2</sup>)
- 空间复杂度：O(1)
- 稳定性：不稳定
- 内排序：Y

##### 代码实现

```java
    public static void selectSort(int[] array) {
        for (int i = 0; i < array.length - 1; i++) {
            int min = i;
            for (int j = i + 1; j < array.length; j++) {
                if (array[j] < array[min]) {
                    min = j;
                }
            }
            int temp = array[i];
            array[i] = array[min];
            array[min] = temp;
        }
    }
```

#### 插入排序

- 时间复杂度：O(n<sup>2</sup>)
- 空间复杂度：O(1)
- 稳定性：稳定
- 内排序：Y

##### 代码实现

```java
    public static void insertSort(int[] array) {
        for (int i = 1; i < array.length; i++) {
            int temp = array[i];
            int j = i;
            while (j > 0 && temp < array[j - 1]) {
                array[j] = array[j - 1];
                j--;
            }
            if (i != j) {
                array[j] = temp;
            }
        }
    }
```

#### 希尔排序

- 时间复杂度：O(nlogn)
- 空间复杂度：O(1)
- 稳定性：不稳定
- 内排序：Y

##### 算法思路

选择一个增量序列 t<sub>1</sub>，t<sub>2</sub>，……，t<sub>k</sub>，其中 t<sub>i</sub> > t<sub>j</sub>, t<sub>k</sub> = 1；

按增量序列个数 k，对序列进行 k 趟排序；

每趟排序，根据对应的增量 t<sub>i</sub>，将待排序列分割成若干长度为 m 的子序列，分别对各子表进行直接插入排序。仅增量因子为 1 时，整个序列作为一个表来处理，表长度即为整个序列的长度。

##### 代码实现

```java
    public static void shellSort(int[] array) {
        int gap = 1;
        while (gap < array.length) {
            gap = gap * 3 + 1;
        }
        while (gap > 0) {
            System.out.println(gap);
            for (int i = gap; i < array.length; i++) {
                int temp = array[i];
                int j = i - gap;
                while (j >= 0 && array[j] > temp) {
                    array[j + gap] = array[j];
                    j -= gap;
                }
                array[j + gap] = temp;
            }
            gap = (int) Math.floor(gap / 3);
        }
    }
```

#### 归并排序

- 时间复杂度：O(nlogn)
- 空间复杂度：O(n)
- 稳定性：稳定
- 内排序：N

归并排序（Merge sort）是建立在归并操作上的一种有效的排序算法。该算法是采用分治法（Divide and Conquer）的一个非常典型的应用。

作为一种典型的分而治之思想的算法应用，归并排序的实现由两种方法：

- 自上而下的递归（所有递归的方法都可以用迭代重写，所以就有了第 2 种方法）；
- 自下而上的迭代；

递归和迭代相比较，特定场景下，递归方法可能不适用；例如在JavaScript中递归的算法深度会比较深，是语言所不能承受的。递归方法会导致很频繁的自调用。一个长度为n的数组最终会调用mergeSort() `2*n-1`次，这意味着如果需要排序的数组长度很大会在某些栈小的浏览器上发生栈溢出错误。尽管迭代的归并排序算法比递归实现要慢一些，但它并不会像递归那样受调用栈限制的影响。把递归算法改用迭代实现是实现栈溢出错误的方法之一

##### 算法思路

1. 申请空间，使其大小为两个已经排序序列之和，该空间用来存放合并后的序列；
2. 设定两个指针，最初位置分别为两个已经排序序列的起始位置；
3. 比较两个指针所指向的元素，选择相对小的元素放入到合并空间，并移动指针到下一位置；
4. 重复步骤 3 直到某一指针达到序列尾；
5. 将另一序列剩下的所有元素直接复制到合并序列尾。

![](http://images.wpt6.cn/blog/2020-09-01-22-40-46.jpg)

##### 代码实现

```java
    public static void mergeSort(int[] array) {
        int[] temp = new int[array.length];
        sort(0, array.length - 1, array, temp);
    }

    public static void sort(int left, int right, int[] array, int[] temp) {
        if (left < right) {
            int mid = (left + right) / 2;
            sort(left, mid, array, temp);
            sort(mid + 1, right, array, temp);
            merge(left, mid, right, array, temp);
            System.out.println(Arrays.toString(temp));
        }
    }

    public static void merge(int left, int mid, int right, int[] array, int[] temp) {
        int i = left, j = mid + 1, t = 0;
        while (i<=mid && j<=right){
            if(array[i]<=array[j]){
                temp[t] = array[i];
                t++;i++;
            }else {
                temp[t] = array[j];
                t++;j++;
            }
        }
        while (i<=mid){
            temp[t++] = array[i++];
        }
        while (j<=right){
            temp[t++] = array[j++];
        }
        t = 0;
        while (left<=right){
            array[left++] = temp[t++];
        }
    }
```

#### 快速排序

- 时间复杂度：O(nlogn)
- 空间复杂度：O(logn)
- 稳定性：不稳定
- 内排序：Y

> *快速排序的最坏运行情况是 O(n²)，比如说顺序数列的快排。但它的平均期望时间是 O(nlogn)，且 O(nlogn) 记号中隐含的常数因子很小，比复杂度稳定等于 O(nlogn) 的归并排序要小很多。所以，对绝大多数顺序性较弱的随机数列而言，快速排序总是优于归并排序。*

#### 堆排序

#### 计数排序

#### 桶排序

#### 基数排序




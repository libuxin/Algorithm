### 学习算法思想，修炼变成内功

为什么要学习**O(n^2)**的排序算法

1.基础，编码简单

2.作为子过程衍生复杂排序算法

3.在某些情况下更加有效

#### 选择排序 Selection Sort

依次寻找最小的元素放到指定位置

```
//选择排序
template<typename T>
void selectionSort(T arr[], int n) {
    for (int i = 0; i < n; i++) {
        // 寻找[i, n)区间里的最小值
        int minIndex = i;
        for (int j = i + 1; j < n; j++)
            if (arr[j] < arr[minIndex])
                minIndex = j;
        swap(arr[i], arr[minIndex]);
    }
}
```
#### 插入排序 Insertion Sort
选择元素位置与前方元素进行两两对比进行排序
```
//插入排序
template<typename T>
void insertionSort(T arr[],int n){
    for(int i=1;i<n;i++){
        //寻找元素arr[i]合适的插入位置
        for(int j=i;j>0 && arr[j]<arr[j-1];j--){
                swap(arr[j],arr[j-1])
        }
    }
}
```
#### 改进插入排序 Insertion Sort
选择元素进行复制与前进行对比，需要交换进行赋值。
```
//插入排序
template<typename T>
void insertionSort(T arr[],int n){
    for(int i=1;i<n;i++){
        //寻找元素arr[i]合适的插入位置
        T e = arr[i];
        int j;//保存元素e应该插入的位置
        for(j=i;j>0 && arr[j-1]>e;j--){
                arr[j]=arr[j-1];
        }
        arr[j] = e;
    }
}
```
优化思路：对满足条件的进行退出。




选择排序和插入排序比较
选择排序不论何种情况都需要完全进行选择。

插入排序在数据近乎有序的情况下复杂度近乎**O(n)**，排序更加快速。更易作为子排序算法。


#### 冒泡排序 Bubble Sort
将元素右移
```
//冒泡排序
template<typename T>
void bubbleSort(T arr[],int n){
    bool isSorted = true;
    for(int i=0;i<n;i++){//外层循环趟数，总趟数为数组长度
        for(int j= 0;j<n-1-i;j++){
            if(arr[j]>arr[j+1]){
                int temp=arr[j];
                arr[j]=arr[j+1];
                arr[j+1]=temp;
                isSorted = false;
            }
        }
        if(isSorted){
            break;
        }
    }
}
```



希尔排序




 复杂度O(nlog(n))的排序算法
#### 归并排序 Merge Sort
```
/*

 * 归并排序大致思路如下：

 *  将数组二分，二分，直到分成只有一个元素的数组（可以简单的计算出层级其实就是log（N））

 *  然后对两个最小单位的数组进行合并操作

 *  直到完成全部的操作

 *  过程中还需要用到一个临时空间，所以归并排序对内存空间是有一定的消耗的

 *  它的思想其实是说将两个已经排好序的数组合并成一个有序的数组

 *  这里再简单的说下Nlog（N）级别算法的简单思想其实就是：

 *  将序列分成log（N）的层级，再对每个层级进行O(N)级别的算法来处理

 * */



// 将 arr[l...mid] 和 arr[mid+1...r] 两部分进行归并
template <typename T>
void __merge(T arr[], int l, int mid, int r)
{
    // 经测试，传递 aux数组的性能效果不好
    T aux[r-l+1];
    for (int i = l; i <= r; ++i) {
        aux[i-l] = arr[i];
    }
    int i = l, j = mid + 1;
    for (int k = l; k <= r; ++k) {
        if (i > mid) {
            arr[k] = aux[j-l];
            ++j;
        } else if (j > r) {
            arr[k] = aux[i-l];
            ++i;
        } else if (aux[i-l] < aux[j-l]) {
            arr[k] = aux[i-l];
            ++i;
        } else {
            arr[k] = aux[j-l];
            ++j;
        }
    }
}



// 递归使用归并排序，对arr[l...r]的范围进行排序
template <typename T>
void __mergeSort(T arr[], int l, int r)
{
    if (l >= r) {
        return;
    }
    int mid = (l + r) / 2;
    __mergeSort(arr, l, mid);
    __mergeSort(arr, mid+1, r);
	//if(arr[mid]>arr[mid+1]) 在数组有可能近乎有序时能提高效率
    __merge(arr, l, mid ,r);

}




template <typename T>
void mergeSort(T arr[], int n)
{
    __mergeSort(arr, 0, n-1);
}

```


在数据近乎有序时，插入排序效率更高，会降到O（n）的复杂度

在数据无序时，归并排序更有效。



# 堆排序

什么是堆？ **堆**是一棵**顺序存储**的**完全二叉树**。

其中每个结点的关键字都**不大于**其孩子结点的关键字，这样的堆称为**小根堆**。

其中每个结点的关键字都**不小于**其孩子结点的关键字，这样的堆称为**大根堆**。

定义：

**大顶堆：arr\[i\] &gt;= arr\[2i+1\] && arr\[i\] &gt;= arr\[2i+2\]  **

**小顶堆：arr\[i\] &lt;= arr\[2i+1\] && arr\[i\] &lt;= arr\[2i+2\]  **

一般**升序**使用大根堆，降序使用小根堆。

这个算法思想可以分成两步：

1. 根据初始数组去**构造初始堆**（构建一个完全二叉树，保证所有的父结点都比它的孩子结点数值大）。
2. 每次**交换第一个和最后一个元素，输出最后一个元素**（最大值），然后把剩下元素**重新调整**为大根堆。

### 构造初始堆示意图![](/assets/heap_sort.jpg)构造初始堆

基本想法是把小的数“沉”下去（叶子节点可以跳过，很明显，所以要从第一个非叶子节点开始，从n/2 - 1开始）

### 

Javascript实现：

    function heapAjust(arr, parent, length) {
        let temp = arr[parent]; // temp保存当前父节点
        let child = 2 * parent + 1; // 先获得左孩子

        while (child < length) {
            // 如果有右孩子结点，并且右孩子结点的值大于左孩子结点，则选取右孩子结点
            if (child + 1 < length && arr[child] < arr[child + 1]) {
                child++;
            }

            // 如果父结点的值已经大于孩子结点的值，则直接结束
            if (temp >= arr[child])
                break;

            // 把孩子结点的值赋给父结点
            arr[parent] = arr[child];

            // 选取孩子结点的左孩子结点,继续向下筛选
            parent = child;
            child = 2 * child + 1;
        }

        arr[parent] = temp;
    }


    function heapSort(arr) {
        // 循环建立初始堆
        for (let i = Math.ceil(arr.length / 2) - 1; i >= 0; i--) {
            heapAjust(arr, i, arr.length);
        }

        // 进行n-1次循环，完成排序
        for (let i = arr.length - 1; i > 0; i--) {
            // 最后一个元素和第一元素进行交换
            let temp = arr[i];
            arr[i] = arr[0];
            arr[0] = temp;

            // 筛选 R[0] 结点，得到i-1个结点的堆
            heapAjust(arr, 0, i);
            console.log(`第 ${arr.length - i} 趟: \t`);
            console.log(arr);
        }
    }


    let arr = [1, 3, 4, 5, 2, 6, 9, 7, 8, 0];
    heapSort(arr);




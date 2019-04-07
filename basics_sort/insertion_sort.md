# 直接插入排序

这个排序的原理就是往一个**小的有序区再插入一个数**，小的有序区，从长度为1的数组开始

![](http://upload-images.jianshu.io/upload_images/3193867-28a43b5f4dd10782.gif?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

javascript实现

```text
function insertionSort(arr) {
    if(arr.length === 1) {
        return;
    }
    for(let i = 1; i < arr.length; i++) {
        let temp = arr[i];
        let j = i - 1;
        while(j >= 0 && arr[j] > temp) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = temp;
    }
}
let arr = [1, -2, 0, -1, 4, -200, 20];
insertionSort(arr);
console.log(arr);
```


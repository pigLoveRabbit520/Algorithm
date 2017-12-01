# 选择排序

原理：每次遍历的时候选择出无序区中最小值或最大值放到有序区

javascript实现：

```
function selectionSort(arr) {
    if(arr.length === 1) {
        return;
    }
    for(let i = 0; i < arr.length - 1; i++) {
        let temp = arr[i];
        let index = i;
        for(let j = i + 1; j < arr.length; j++) {
            if(arr[j] < temp) {
                temp = arr[j];
                index = j;
            }
        }
        if(index != i) {
            arr[index] = arr[i];
            arr[i] = temp;
        }
    }
}
let arr = [1, -2, 0, -1, 4, -200, 20];
selectionSort(arr);
console.log(arr);
```




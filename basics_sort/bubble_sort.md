# 冒泡排序

这个排序方法是一个很简单的**交换排序（还有快速排序等）**

两两交换，每次走一趟的时候把最大的数放到末尾，然后区域长度缩短一位，递归下去

javascript实现：

```javascript
function bubbleSort(arr) {
    if(arr.length === 1) {
        return;
    }
    for(let i = arr.length - 1; i >= 1; i--) {
        for(let j = 0; j < i; j++) {
            if(arr[j] > arr[j + 1]) {
                let temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }    
    }
}
let arr = [1, -2, 0, -1, 4, -200, 20];
bubbleSort(arr);
console.log(arr);
```

另一种写法：

```java
public static void bubbleSort(int[] numbers)
{
    int temp = 0;
    int size = numbers.length;
    for(int i = 0 ; i < size-1; i ++)
    {
        for(int j = 0 ;j < size-1-i ; j++)
        {
            if(numbers[j] > numbers[j+1])  //交换两数位置
            {
            temp = numbers[j];
            numbers[j] = numbers[j+1];
            numbers[j+1] = temp;
            }
        }
    }
}
```


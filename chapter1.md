# 快速排序

快速排序应用了**分治**策略，详细介绍可以移步这里[Just for fun——迅速写完快速排序](https://segmentfault.com/a/1190000012024678)

# 高效写法

现贴上**PHP**实现：

```
<?php

$arr = [2, -1, -2, 100, 5];


function quickSort(&$arr, $start, $end) {
    if($end - $start === 1) {
        if($arr[$start] > $arr[$end]) {
            $temp = $arr[$start];
            $arr[$start] = $arr[$end];
            $arr[$end] = $temp;
        }
    } elseif ($end - $start > 1) {
        $middle = $arr[$start];
        $i = $start;
        $j = $end;
        while ($i !== $j && $i <= $end && $j >= $start) {
            while ($arr[$j] >= $middle && $j > $i) {
                $j--;
            }
            if($j > $i) {
                $arr[$i] = $arr[$j];
                $i++;
            }
            while ($arr[$i] <= $middle && $i < $j) {
                $i++;
            }
            if($i < $j) {
                $arr[$j] = $arr[$i];
                $j--;
            }
        }
        $arr[$i] = $middle;
        quickSort($arr, $start, $i - 1);
        quickSort($arr, $i + 1, $end);
    }
}

quickSort($arr, 0, count($arr) - 1);
print_r($arr);
```

Javascript实现：

```
let arr = [2, -1, -2, 100, 5];

function quickSort(arr, start, end) {
    if(end - start === 1) {
        if(arr[start] > arr[end]) {
            let temp = arr[start];
            arr[start] = arr[end];
            arr[end] = temp;
        }
    } else if (end - start > 1) {
        let middle = arr[start];
        let i = start;
        let j = end;
        while (i !== j && i <= end && j >= start) {
            while (arr[j] >= middle && j > i) {
                j--;
            }
            if(j > i) {
                arr[i] = arr[j];
                i++;
            }
            while (arr[i] <= middle && i < j) {
                i++;
            }
            if(i < j) {
                arr[j] = arr[i];
                j--;
            }
        }
        arr[i] = middle;
        quickSort(arr, start, i - 1);
        quickSort(arr, i + 1, end);
    }
}

quickSort(arr, 0, arr.length - 1);
console.log(arr);
```

## 另一种简单写法

这种写法就是每次都从头遍历数组，小于等于中间量的数放**小于等于数组**，大于中间量的数放一个**大于数组**，然后再对这两个数组继续递归，直到达到递归停止点

PHP版本

```
<?php

$arr = [2, -1, -2, 100, 5];


function quickSort($arr) {
    if(empty($arr) || count($arr) <= 1) {
        return $arr;
    }
    $len = count($arr);
    $indexMiddle = floor($len / 2);
    $middle = $arr[$indexMiddle];
    $arrLess = [];
    $arrGreater = [];
    for ($i = 0; $i < $len; $i++) { 
        if($i != $indexMiddle && $arr[$i] <= $middle) {
            array_push($arrLess, $arr[$i]);
        }

    }
    for ($j = 0; $j < $len; $j++) { 
        if($j != $indexMiddle && $arr[$j] > $middle) {
            array_push($arrGreater, $arr[$j]);
        }
    }
    return array_merge(
        quickSort($arrLess), 
        [$middle], 
        quickSort($arrGreater)
    );
}

print_r(quickSort($arr));
```

Javacript版本

```
let arr = [2, -1, -2, 100, 5];


function quickSort(arr) {
    if(!arr || arr.length <= 1) {
        return arr;
    }
    let indexMiddle = Math.floor(arr.length / 2);
    let middle = arr[indexMiddle];
    let arrLess = [];
    let arrGreater = [];
    for (let i = 0; i < arr.length; i++) { 
        if(i != indexMiddle && arr[i] <= middle) {
            arrLess.push(arr[i]);
        }

    }
    for (let j = 0; j < arr.length; j++) {
        if(j != indexMiddle && arr[j] > middle) {
            arrGreater.push(arr[j]);
        }
    }
    return quickSort(arrLess).concat(middle, quickSort(arrGreater));
}


console.log(quickSort(arr));
```

Python版本（简短很多，果然是”人生苦短，快用python“）

```
import math

def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[math.floor(len(arr) / 2)]
    left = [x for x in arr if x < pivot]
    middle = [pivot]
    right = [x for x in arr if x > pivot]
    return quicksort(left) + middle + quicksort(right)
    
print( quicksort([3,6,8,10,1,2,1]) )
```




# 快速排序

快速排序应用了**分治**策略

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




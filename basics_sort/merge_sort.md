# 归并排序



go实现：

```
package main

import (
	"fmt"
)

// 核心代码
func Merge(arr []int, low int, mid int, high int) {
	i := low
	j := mid + 1
	k := 0
	arrNew := make([]int, high-low+1)
	for i <= mid && j <= high {
		if arr[i] <= arr[j] {
			arrNew[k] = arr[i]
			i++
			k++
		} else {
			arrNew[k] = arr[j]
			j++
			k++
		}
	}
	// 若第一段序列还没扫描完，将其全部复制到合并序列
	for i <= mid {
		arrNew[k] = arr[i]
		i++
		k++
	}
	// 若第二段序列还没扫描完，将其全部复制到合并序列
	for j <= high {
		arrNew[k] = arr[j]
		j++
		k++
	}
	k = 0
	i = low
	for i <= high {
		arr[i] = arrNew[k]
		i++
		k++
	}
}

func MergePass(arr []int, gap int, length int) {
	i := 0
	// 归并gap长度的两个相邻子表
	for ; i+2*gap-1 < length; i = i + 2*gap {
		Merge(arr, i, i+gap-1, i+2*gap-1)
	}
	// 有两种情况
	// 余下两个子表，后者长度小于gap
	if i+gap-1 < length {
		Merge(arr, i, i+gap-1, length-1)
	}
}

func MergeSort(arr []int) {
	arrLen := len(arr)
	for gap := 1; gap < arrLen; gap *= 2 {
		MergePass(arr, gap, arrLen)
		fmt.Printf("gap = %v \t", gap)
		fmt.Println(arr)
	}
}

func main() {
	arr := []int{2, 4, -1, 0, 7, 1, 9}
	MergeSort(arr)
}

```




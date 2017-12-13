# 希尔排序

这个算法其实是在直接插入排序的基础上进行**分组**。将整个待排元素序列切割成若干个子序列（由相隔某个“**增量**”的元素组成的）分别进行直接插入排序，然后依次缩减增量再进行排序，待整个序列中的元素基本有序（增量足够小，最后变为1，相当于进行一次插入排序）时，再对全体元素进行一次直接插入排序。

**javascript实现**

```
// 步长越大分组越多
function shellSort(arr) {
    for (let gap = Math.floor(arr.length / 2); gap > 0; gap = Math.floor(gap / 2)) {
        // 共gap个组，对每一组都执行直接插入排序
        for (let i = 0; i < gap; i++) {
            for(let j = i + gap; j < arr.length; j += gap) {
                let temp = arr[j];
                let k = j - gap;
                while(k >= 0 && arr[k] > temp) {
                    arr[k + gap] = arr[k];
                    k -= gap;
                }
                arr[k + gap] = temp;
            }
        }
    }
}




let arr = [1, -2, 0, -1, 4, -200, 20];
shellSort(arr);
```

**go语言实现**

```
package main

import (
	"fmt"
)

func shellSort(arr []int) {
	arrLen := len(arr)
	// 设置步长
	for gap := arrLen / 2; gap > 0; gap /= 2 {
		for i := 0; i < gap; i++ {
			for j := i + 1; j < arrLen; j += gap {
				temp := arr[j]
				k := j - 1
				for k >= 0 && arr[k] > temp {
					arr[k+1] = arr[k]
					k--
				}
				arr[k+1] = temp
			}
		}
	}
}

func main() {
	arr := []int{2, 4, -1, 8}
	shellSort(arr)
	fmt.Println(arr)
}
```




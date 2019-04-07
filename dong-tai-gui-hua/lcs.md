---
description: 最长公共子序列问题
---

# LCS

### 问题描述

递归解法

```text
package main

import "fmt"

func max(x, y int) int {
	if x > y {
		return x
	}
	return y
}

func LongestCommonSequence(a string, b string) int {
	aChars := []rune(a)
	bChars := []rune(b)
	aLen := len(aChars)
	bLen := len(bChars)
	if aLen == 0 || bLen == 0 {
		return 0
	}
	if aChars[aLen-1] == bChars[bLen-1] {
		return LongestCommonSequence(string(aChars[:aLen-1]), string(bChars[:bLen-1])) + 1
	} else {
		return max(
			LongestCommonSequence(string(aChars[:aLen-1]), b),
			LongestCommonSequence(a, string(bChars[:bLen-1])))
	}
}
```

### 动态规划

```text
package main

import "fmt"

func max(x, y int) int {
	if x > y {
		return x
	}
	return y
}

func LongestCommonSequenceDP(a string, b string) int {
	aChars := []rune(a)
	bChars := []rune(b)
	aLen := len(aChars)
	bLen := len(bChars)
	if aLen == 0 || bLen == 0 {
		return 0
	}

	record := make([][]int, aLen+1)
	for i := 0; i <= aLen; i++ {
		record[i] = make([]int, bLen+1)
		record[i][0] = 0
	}

	for j := 0; j <= bLen; j++ {
		record[0][j] = 0
	}

	for i := 1; i <= aLen; i++ {
		for j := 1; j <= bLen; j++ {
			if aChars[i-1] == bChars[j-1] {
				record[i][j] = record[i-1][j-1] + 1
			} else {
				record[i][j] = max(record[i][j-1], record[i-1][j])
			}
		}
	}

	return record[aLen][bLen]
}

func main() {
	a := "ACDE"
	b := "CBE"
	fmt.Printf("Longest sub sequence length of %s and %s is %d\n", a, b,
		LongestCommonSequenceDP(a, b))
}

```


---
description: https://leetcode.com/problems/jump-game-ii/
---

# 跳跃游戏 II

### 题目 <a href="#ti-mu" id="ti-mu"></a>

\
给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

你的目标是使用最少的跳跃次数到达数组的最后一个位置。

示例:

```
输入: [2,3,1,1,4]
输出: 2
解释: 跳到最后一个位置的最小跳跃数是 2。
     从下标为 0 跳到下标为 1 的位置，跳 1 步，然后跳 3 步到达数组的最后一个位置。
```

说明:

假设你总是可以到达数组的最后一个位置。

### 思路  <a href="#si-lu-2" id="si-lu-2"></a>

最基本的思路，可能是从前往后遍历。

以 `[2,3,1,1,4]` 作为例子。

我们第一次可以选择走两步：

（1）直接两步，可以走到 1，

（2）走一步，选择走到3，然后向后走走3步。

如果用贪心的角度思考的话，肯定是方案 2 划算一点。

每次走最远的地方

然后我们一直按照这个方式，走到最后。

其中方案能走的最远的地方，我们可以定义为边界。

#### java 实现 <a href="#java-shi-xian-1" id="java-shi-xian-1"></a>

最核心的就是一句话，如何达到可以达到的最远距离呢？

```java
public int jump(int[] nums) {
    int count = 0;
    if(nums.length == 1) {
        return count;
    }
    // 目前能跳到的最远位置
    int maxFar = 0;
    // 上次跳跃可达范围右边界（下次的最右起跳点）
    int end = 0;
    // 最后一个位置不需要访问。
    for(int i = 0; i < nums.length-1; i++) {
        maxFar = Math.max(maxFar, i + nums[i]);
        // 到达上次跳跃能到达的右边界了
        if(i == end) {
            // 更新右边界
            end = maxFar;
            count++;
        }
    }
    return count;
}

```

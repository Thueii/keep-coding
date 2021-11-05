# 接雨水

Link => [有效的括号](https://leetcode-cn.com/problems/trapping-rain-water/)

给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

>输入：height = [0,1,0,2,1,0,1,3,2,1,2,1]<br />
>输出：6<br />
>在这种情况下，可以接 6 个单位的雨水（蓝色部分表示雨水）。 <br />

> 示例 2：<br />
>输入：height = [4,2,0,3,2,5]<br />
>输出：9<br />

执行结果：
通过
显示详情

添加备注
执行用时：6732 ms, 在所有 Python3 提交中击败了5.02% 的用户
内存消耗：17 MB, 在所有 Python3 提交中击败了5.06% 的用户
通过测试用例：320 / 320
```python
class Solution:
    def trap(self, height: List[int]) -> int:
        dp = [[max(height), max(height), 0] for i in range(len(height))]
        for index in range(len(height)):
            if index == 0:
                dp[index][0] = 0
                if height[index] == dp[index][1]:
                    if index + 1 < len(height):
                        dp[index][1] = max(height[index+1::])
                    else:
                        dp[index][1] = 0
                continue

            if height[index - 1] > dp[index - 1][0]:
                dp[index][0] = height[index - 1]
            else:
                dp[index][0] = dp[index - 1][0]
            
            if height[index] < dp[index - 1][1]:
                dp[index][1] = dp[index - 1][1]
            else:
                if index + 1 < len(height):
                    dp[index][1] = max(height[index+1::])
                else:
                    dp[index][1] = 0

            if not (height[index] >= dp[index][0] or height[index] >= dp[index][1]):
                dp[index][2] = 1

        s = 0
        for index in range(len(dp)):
            if dp[index][2] == 1:
                s += min(dp[index][0], dp[index][1]) - height[index]
        return s
```
改进：

执行结果：
通过
显示详情

添加备注
执行用时：40 ms, 在所有 Python3 提交中击败了76.80% 的用户
内存消耗：15.8 MB, 在所有 Python3 提交中击败了69.47% 的用户
通过测试用例：320 / 320
```python
class Solution:
    def trap(self, height: List[int]) -> int:
        p1, p2 = 0, len(height) - 1
        dp1 = [0] * len(height)
        dp2 = [0] * len(height)
 
        while True:
            if p1 == len(height):
                break
            if p1 >= 1:
                dp1[p1] = max(dp1[p1 - 1], height[p1])
                dp2[p2] = max(dp2[p2 + 1], height[p2])
            else:
                dp1[p1] = height[p1]
                dp2[p2] = height[p2]
            p1 += 1
            p2 -= 1

        s = 0
        for index in range(len(height)):
            if height[index] >= dp1[index] or height[index] >= dp2[index]:
                continue
            else:
                s += min(dp1[index],dp2[index]) - height[index]
            
        return s
```
**Tag: 栈、数组、双指针、动态规划、单调栈**

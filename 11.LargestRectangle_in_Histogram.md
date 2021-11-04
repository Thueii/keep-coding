# 柱状图中最大的矩形

Link => [柱状图中最大的矩形](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/)

给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。求在该柱状图中，能够勾勒出来的矩形的最大面积。

>输入：heights = [2,1,5,6,2,3]<br />
>输出：10<br />

> 示例 2：<br />
>输入：heights = [2,4]<br />
>输出：2<br />

执行结果：
超出时间限制
显示详情

添加备注
最后执行的输入：
[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1
查看全部
```python
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        # dp表示比当前小的左右的第一个的索引位置
        p1 = 0
        p2 = len(heights) - 1
        dp1 = [p1] * len(heights)
        dp2 = [p2] * len(heights)

        while True:
            if p1 == len(heights):
                break

            if p1 == 0:
                dp1[p1] = p1 - 1
                dp2[p2] = p2 + 1
                p1 += 1
                p2 -= 1
                continue

            if heights[p1] > heights[p1 - 1]:
                dp1[p1] = p1 - 1
            else:
                if dp1[p1 - 1] >= 0 and heights[p1] > heights[dp1[p1 - 1]]:
                    dp1[p1] = dp1[p1 - 1]
                else:
                    left_list = heights[:p1]
                    dp1[p1] = -1
                    while True:
                        if len(left_list) >= 1:
                            if (left_list.pop() < heights[p1]):
                                dp1[p1] = len(left_list)
                                break
                        else:
                            break

            if heights[p2] > heights[p2 + 1]:
                dp2[p2] = p2 + 1
            else:
                if dp2[p2 + 1] < len(heights) and heights[p2] > heights[dp2[p2 + 1]]:
                    dp2[p2] = dp2[p2 + 1]
                else:
                    right_list = heights[p2+1:]
                    dp2[p2] = len(heights)
                    for index in range(len(right_list)):
                        if right_list[index] < heights[p2]:
                            dp2[p2] = p2 + index + 1
                            break
            p1 += 1
            p2 -= 1

        s = 0
        for index in range(len(heights)):
            
            temp_s = (dp2[index] - dp1[index] - 1) * heights[index]
            s = max(temp_s, s)

        return s
```
改进：

执行结果：
通过
显示详情

添加备注
执行用时：232 ms, 在所有 Python3 提交中击败了60.54% 的用户
内存消耗：25.8 MB, 在所有 Python3 提交中击败了19.20% 的用户
通过测试用例：96 / 96
```python
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        # 单调栈
        # 用顺序来确定左边界，用判断大小来确定右边界
        stack = []
        s = []
        for index in range(len(heights)):
            if index == 0:
                stack.append(index)
            else:
                if len(stack) > 0:
                    if heights[stack[-1]] <= heights[index]:
                        stack.append(index)
                    else:
                        while len(stack) > 0:
                            if heights[stack[-1]] > heights[index]:
                                now = heights[stack.pop()]
                                if len(stack) == 0:
                                    s.append((index-(-1)-1)*now)
                                else:
                                    s.append((index-stack[-1]-1)*now)
                            else:
                                break
                        stack.append(index)
        while len(stack) > 1:
            now = stack.pop()
            s.append(((len(heights))-stack[-1]-1)*heights[now])
        if len(stack) == 1:
            now = stack.pop()
            s.append(((len(heights))-(-1)-1)*heights[now])
        return max(s)
                        
```
改进：
```python
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        heights.append(0)       #哨兵，防止不计算
        n = len(heights)

        res = 0

        stk = []        #左侧第一个比当前小的位置
        for i in range(n):
            x = heights[i]
            while stk and heights[stk[-1]] >= x:
                h = heights[stk.pop(-1)]
                l = stk[-1] + 1 if stk else 0
                r = i - 1
                cur = (r - l + 1) * h
                res = max(res, cur)
            
            stk.append(i)
        
        return res

```
**Tag: 栈、数组、单调栈**

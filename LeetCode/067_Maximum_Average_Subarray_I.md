# 子数组最大平均数 I

Link => [子数组最大平均数 I](https://leetcode-cn.com/problems/maximum-average-subarray-i/)

## 题目
给你一个由 n 个元素组成的整数数组 nums 和一个整数 k 。

请你找出平均数最大且 长度为 k 的连续子数组，并输出该最大平均数。

任何误差小于 10-5 的答案都将被视为正确答案。

**示例1**
>输入：nums = [1,12,-5,-6,50,3], k = 4<br />
>输出：12.75<br />
>解释：最大平均数 (12-5-6+50)/4 = 51/4 = 12.75<br />

**示例2**
>输入：nums = [5], k = 1<br />
>输出：5.00000<br />

**执行结果：通过 显示详情**
感觉很不好因为每次都要又重头找

- 执行用时：208 ms, 在所有 Python3 提交中击败了51.43% 的用户
内存消耗：23.8 MB, 在所有 Python3 提交中击败了57.45% 的用户
通过测试用例：127 / 127

```python
class Solution:
    def findMaxAverage(self, nums: List[int], k: int) -> float:
        start = sum(nums[:k])
        s = 0
        e = k
        res = start
        while e < len(nums):
            cur = start-nums[s]+nums[e]
            res = max(res, cur)
            s += 1
            e += 1
            start = cur
        return res/k
```
**改进**
简单方法

```python
class Solution:
    def findMaxAverage(self, nums, k):
        i = 0
        total = sum(nums[:k])
        tmp = sum(nums[:k])
        for num in nums[k:]:
            tmp = tmp - nums[i] + num
            total = max(total, tmp)
            i += 1
        return total / k
```

**Tag: 数组、滑动窗口**

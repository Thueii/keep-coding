# 最大子序和

Link => [最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)

## 题目
给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

**示例1**
>输入：ms = [-2,1,-3,4,-1,2,1,-5,4]<br />
>输出：[3,9,20,null,null,15,7]<br />
>解释：连续子数组 [4,-1,2,1] 的和最大，为 6 。<br />

**执行结果：通过 显示详情**

- 执行用时：136 ms, 在所有 Python3 提交中击败了41.61% 的用户
内存消耗：26.1 MB, 在所有 Python3 提交中击败了5.10% 的用户
通过测试用例：209 / 209

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        # 第一感觉动态规划最容易想，但是确实比较费空间

        dp = [0 for num in nums]
        for i in range(len(nums)):
            if i == 0:
                dp[i] = nums[i]
            else:
                if dp[i-1] < 0:
                    dp[i] = nums[i]
                else:
                    dp[i] = nums[i] + dp[i-1]
        return max(dp)
```
**改进：**

- 执行用时：120 ms, 在所有 Python3 提交中击败了48.28% 的用户
内存消耗：25.4 MB, 在所有 Python3 提交中击败了31.33% 的用户
通过测试用例：209 / 209
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        # 把动态规划改了改，怎么还是很慢呢

        for i in range(len(nums)):
            if i == 0:
                sum_max = nums[0]
                last = nums[0]
            else:
                if last < 0:
                    last = nums[i]
                else:
                    last += nums[i]
                sum_max = max(sum_max, last)
        return sum_max
```
**Tag: 树、深度优先搜索、二叉树**

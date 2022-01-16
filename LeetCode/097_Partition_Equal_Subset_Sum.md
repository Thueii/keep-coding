# 分割等和子集

Link => [分割等和子集](https://leetcode-cn.com/problems/partition-equal-subset-sum/)

## 题目

    给你一个 只包含正整数 的 非空 数组 nums 。请你判断是否可以将这个数组分割成两个子集，使得两个子集的元素和相等。

**示例1**

    输入：nums = [1,5,11,5]
    输出：true
    解释：数组可以分割成 [1, 5, 5] 和 [11] 。

**示例2**

    输入：nums = [1,2,3,5]
    输出：false
    解释：数组不能分割成两个元素和相等的子集。

**执行结果：通过 显示详情**
记忆化搜索，注意target一定要减半，这样省一半时间，否则你要做到最后一个才知道结果

- 执行用时：124 ms, 在所有 Python3 提交中击败了98.00% 的用户
内存消耗：21.2 MB, 在所有 Python3 提交中击败了43.69% 的用户
通过测试用例：117 / 117

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        target = sum(nums)
        if target %2:
            return False
        target = target // 2

        def dfs(nums, i, left):
            if left == 0:
                return True
            if left < 0 or i == len(nums) or left in dp[i]:
                return False
            if dfs(nums, i+1, left-nums[i]) or dfs(nums, i+1, left):
                return True
            dp[i].add(left)
            return False

        dp = [set() for i in range(len(nums))] # 同一层剩下的数字一样的话，其实结果是一样的，所以记忆化搜索
        return dfs(nums, 0, target)
```
动态规划，实在不太直观，又是啃了好久才看懂，dp[i][j]表示[0,i]区间内是否能有和为j的子串
```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        n = len(nums)
        arr_sum = sum(nums)
        if arr_sum % 2 != 0:
            return False
        target = arr_sum // 2
        dp = [[False] * (target + 1) for _ in range(n)]
        if nums[0] <= target: # >target 就越界了
            dp[0][nums[0]] = True
        for i in range(1, n):
            for j in range(target+1):
                if dp[i-1][j]:
                    dp[i][j] = True
                    continue
                if nums[i] == j:
                    dp[i][j] = True
                    continue
                if nums[i] < j : # 防止j-nums[i]<0
                    if dp[i-1][j-nums[i]]:
                        dp[i][j] = True
        return dp[-1][-1]
```

**Tag: 数组、动态规划**

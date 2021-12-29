# 目标和

Link => [目标和](https://leetcode-cn.com/problems/target-sum/)

## 题目
给你一个整数数组 nums 和一个整数 target 。

向数组中的每个整数前添加 '+' 或 '-' ，然后串联起所有整数，可以构造一个 表达式 ：

    例如，nums = [2, 1] ，可以在 2 之前添加 '+' ，在 1 之前添加 '-' ，然后串联起来得到表达式 "+2-1" 。

返回可以通过上述方法构造的、运算结果等于 target 的不同 表达式 的数目。

**示例1**

    输入：nums = [1,1,1,1,1], target = 3
    输出：5
    解释：一共有 5 种方法让最终目标和为 3 。
    -1 + 1 + 1 + 1 + 1 = 3
    +1 - 1 + 1 + 1 + 1 = 3
    +1 + 1 - 1 + 1 + 1 = 3
    +1 + 1 + 1 - 1 + 1 = 3
    +1 + 1 + 1 + 1 - 1 = 3

**示例2**

    输入：nums = [1], target = 1
    输出：1

**执行结果：通过 显示详情**
。。。回溯。。超时。。没得办法

- 超时

```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        def dfs(idx: int, cur_sum: int) -> None:
            nonlocal res
            if idx == n:
                if cur_sum == target:
                    res += 1
                return 

            dfs(idx + 1, cur_sum + nums[idx])
            dfs(idx + 1, cur_sum - nums[idx])

        n = len(nums)
        res = 0
        dfs(0, 0)
        return res
```
**改进：**
我靠，01背包问题，看答案看了好久才似懂非懂，写出来。。。看了n个解释，终于到这里看懂了。
[通过转换target，无需考虑左右边界，包含一维dp和二维dp两种思路](https://leetcode-cn.com/problems/target-sum/solution/tong-guo-zhuan-huan-targetwu-xu-kao-lu-z-6hjv/)

- 执行用时：96 ms, 在所有 Python3 提交中击败了52.62% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了46.99% 的用户
通过测试用例：139 / 139
```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        sums = sum(nums)
        if sums < abs(target) or (sums + target) % 2:
            return 0
        target = (sums + target) // 2

        n = len(nums)
        dp = [[0] * (target + 1) for _ in range(n)]
        for i in range(n):
            dp[i][0] = 1

        for i in range(n):
            for j in range(target+1):
                if j<nums[i]:
                    dp[i][j] = dp[i-1][j]
                else:
                    dp[i][j] = dp[i-1][j] + dp[i-1][j-nums[i]]
        return dp[n-1][target]

```

**Tag: 数组、动态规划、回溯**

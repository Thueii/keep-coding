# 面试题 08.01. 三步问题

Link => [最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)

## 题目
三步问题。有个小孩正在上楼梯，楼梯有n阶台阶，小孩一次可以上1阶、2阶或3阶。实现一种方法，计算小孩有多少种上楼梯的方式。结果可能很大，你需要对结果模1000000007。

**示例1**
>输入：n = 3 <br />
>输出：4<br />
>解释：有四种走法<br />

**示例2**
>输入：n = 5 <br />
>输出：13<br />

**执行结果：通过 显示详情**

- 执行用时：356 ms, 在所有 Python3 提交中击败了43.06% 的用户
内存消耗：50.5 MB, 在所有 Python3 提交中击败了31.65% 的用户
通过测试用例：32 / 32

```python
class Solution:
    def waysToStep(self, n: int) -> int:
        dp = [0] * n
        if n <= 3:
            return 2**(n-1) 
        dp[0] = 1
        dp[1] = 2
        dp[2] = 4
        for i in range(3, n):
            dp[i] = (dp[i-1] + dp[i-2] + dp[i-3]) % 1000000007
        return dp[n-1] 
```
**改进：**
用三个量存就行了，省空间和查询到数组位置的时间

- 执行用时：200 ms, 在所有 Python3 提交中击败了93.93% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了63.73% 的用户
通过测试用例：32 / 32
```python
class Solution:
    def waysToStep(self, n: int) -> int:
        if n <= 3:
            return 2**(n-1) 
        a = 1
        b = 2
        c = 4
        for i in range(3, n):
            res = (a + b + c) % 1000000007
            a, b, c = b, c, res
        return res

```
**Tag: 记忆化搜索、数学、动态规划**

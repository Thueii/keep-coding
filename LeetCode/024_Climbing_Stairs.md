# 爬楼梯

Link => [爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)
假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

注意：给定 n 是一个正整数。

>输入：2<br />
>输出：2<br />
>解释： 有两种方法可以爬到楼顶。<br />
>1.  1 阶 + 1 阶<br />
>2.  2 阶<br />

>输入：3<br />
>输出：3<br />
>解释： 有三种方法可以爬到楼顶。<br />
>1.  1 阶 + 1 阶 + 1 阶<br />
>2.  1 阶 + 2 阶<br />
>3.  2 阶 + 1 阶<br />

执行结果：
递归
超出时间限制

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        # 递归
        if n < 3:
            return n
        else:
            return self.climbStairs(n - 2) + self.climbStairs(n - 1)
```
改进：
动态规划

执行结果：
通过
显示详情

添加备注
执行用时：28 ms, 在所有 Python3 提交中击败了85.11% 的用户
内存消耗：14.9 MB, 在所有 Python3 提交中击败了71.76% 的用户
通过测试用例：45 / 45

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        # 动态规划，有浪费一些空间的
        dp = [0 for i in range(n + 1)]
        index = 0
        while index <= n:
            if index < 3:
                dp[index] = index
            else:
                dp[index] = dp[index-1] + dp[index-2]
            index += 1
        return dp[-1]
```
改进：
执行结果：
通过
显示详情

添加备注
执行用时：28 ms, 在所有 Python3 提交中击败了85.11% 的用户
内存消耗：14.8 MB, 在所有 Python3 提交中击败了80.79% 的用户
通过测试用例：45 / 45
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        # 除去不必要的存储
        res = 1
        pre = 1
        count = 1
        while count < n:
            temp = res
            res += pre
            pre = temp
            count += 1
        return res
```
改进：
简化代码
执行结果：
通过
显示详情

添加备注
执行用时：20 ms, 在所有 Python3 提交中击败了99.32% 的用户
内存消耗：14.8 MB, 在所有 Python3 提交中击败了87.64% 的用户
通过测试用例：45 / 45
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        res = 1
        pre = 1
        for i in range(2, n + 1):
            pre, res = res, pre + res
        return res
```
**Tag: 记忆化搜索、数学、动态规划**

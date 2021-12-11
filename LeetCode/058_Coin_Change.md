# 零钱兑换

Link => [零钱兑换](https://leetcode-cn.com/problems/coin-change/)

## 题目
给你一个整数数组 coins ，表示不同面额的硬币；以及一个整数 amount ，表示总金额。

计算并返回可以凑成总金额所需的 最少的硬币个数 。如果没有任何一种硬币组合能组成总金额，返回 -1 。

你可以认为每种硬币的数量是无限的。

**示例1**
>输入：coins = [1, 2, 5], amount = 11<br />
>输出：3 <br />
>解释：11 = 5 + 5 + 1<br />

**执行结果：通过 显示详情**
广度优先搜索，哎呀终于明白了，，，，

- 执行用时：660 ms, 在所有 Python3 提交中击败了96.59% 的用户
内存消耗：15.4 MB, 在所有 Python3 提交中击败了22.85% 的用户
通过测试用例：188 / 188

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        stack = [amount]
        adict = {}
        res = 1
        if amount == 0:
            return 0
        while True:
            tmp = []
            while stack:
                cur = stack.pop()
                for i in coins:
                    if cur - i == 0:
                        return res
                    elif cur - i > 0:
                        if not adict.get(cur - i):
                            adict[cur - i] = True
                            tmp.append(cur - i)
            if not tmp:
                return -1
            stack = tmp
            res += 1
```
**改进：**
再用动态规划？ 还和057一样

- 执行用时：1128 ms, 在所有 Python3 提交中击败了41.20% 的用户
内存消耗：15 MB, 在所有 Python3 提交中击败了95.76% 的用户
通过测试用例：188 / 188
```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [10001 for i in range(0, amount+1)]
        dp[0] = 0
        for i in range(1, amount+1):
            for j in coins:
                if i - j >=0:
                    dp[i] = min(dp[i], dp[i-j] + 1)
        if dp[amount] == 10001:
            return -1
        else:
            return dp[amount]            
            
```

**Tag: 广度优先搜索、数组、动态规划**

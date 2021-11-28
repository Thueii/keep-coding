# 我能赢吗

Link => [我能赢吗](https://leetcode-cn.com/problems/can-i-win/)

## 题目
在 "100 game" 这个游戏中，两名玩家轮流选择从 1 到 10 的任意整数，累计整数和，先使得累计整数和达到或超过 100 的玩家，即为胜者。

如果我们将游戏规则改为 “玩家不能重复使用整数” 呢？

例如，两个玩家可以轮流从公共整数池中抽取从 1 到 15 的整数（不放回），直到累计整数和 >= 100。

给定一个整数 maxChoosableInteger （整数池中可选择的最大数）和另一个整数 desiredTotal（累计和），判断先出手的玩家是否能稳赢（假设两位玩家游戏时都表现最佳）？

你可以假设 maxChoosableInteger 不会大于 20， desiredTotal 不会大于 300。

**示例1**
>输入：maxChoosableInteger = 10<br />
>desiredTotal = 11<br />
>输出：false<br />
>无论第一个玩家选择哪个整数，他都会失败。<br />
>第一个玩家可以选择从 1 到 10 的整数。<br />
>如果第一个玩家选择 1，那么第二个玩家只能选择从 2 到 10 的整数。<br />
>第二个玩家可以通过选择整数 10（那么累积和为 11 >= desiredTotal），从而取得胜利.<br />
>同样地，第一个玩家选择任意其他整数，第二个玩家都会赢。<br />

**执行结果：通过 显示详情**

最重要的是，当前不行，选了之后对方不行，那你就行
如果当前先手选了i之后还不能马上赢，但是下一步后手选数字的时候选输了（也就是dfs(cur | state, desiredTotal - i, dp)返回了False），说明先手能赢，dp[state] = True，并返回True

- 执行用时：2268 ms, 在所有 Python3 提交中击败了63.71% 的用户
内存消耗：73.2 MB, 在所有 Python3 提交中击败了67.09% 的用户
通过测试用例：57 / 57

```python
class Solution:
    def canIWin(self, maxChoosableInteger: int, desiredTotal: int) -> bool:
        if maxChoosableInteger >= desiredTotal:
            return True
        if ((1 + maxChoosableInteger) * maxChoosableInteger) / 2 < desiredTotal:
            return False

        def dfs(state, desiredTotal, dp):

            if state in dp:
                return dp[state]
            for i in range(1, maxChoosableInteger + 1):
                cur = 1 << (i-1)
                if cur & state != 0:
                    continue
                elif i >= desiredTotal:
                    dp[state] = True
                    return True
                else:
                    if not dfs(cur|state, desiredTotal - i, dp):
                        dp[state] = True
                        return True
            dp[state] = False
            return False
        return dfs(0, desiredTotal, {})
```

**Tag: 记忆化搜索、位运算、数字、动态规划、状态压缩、博弈**

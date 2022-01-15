# 最佳买卖股票时机含冷冻期

Link => [最佳买卖股票时机含冷冻期](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

## 题目

    给定一个整数数组，其中第 i 个元素代表了第 i 天的股票价格 。
    设计一个算法计算出最大利润。在满足以下约束条件下，你可以尽可能地完成更多的交易（多次买卖一支股票）:

        你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。
        卖出股票后，你无法在第二天买入股票 (即冷冻期为 1 天)。


**示例1**

    输入: [1,2,3,0,2]
    输出: 3 
    解释: 对应的交易状态为: [买入, 卖出, 冷冻期, 买入, 卖出]

**执行结果：通过 显示详情**
动态规划但是只存了最后的状态就够了所以没有用数组，而且动态转移方程设计三种情况所以必须要三个dp来存状态

- 执行用时：36 ms, 在所有 Python3 提交中击败了61.59% 的用户
内存消耗：15.3 MB, 在所有 Python3 提交中击败了57.57% 的用户
通过测试用例：210 / 210

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # 初始化，含第一天
        dp0 = 0 # 手里没股票，不在冷冻期
        dp1 = 0 # 手里没股票，在冷冻期
        dp2 = -prices[0] # 手里有股票  # 等于是买了第一天的

        for i in range(1, len(prices)):
            # 今天
            new_dp0 = max(dp0, dp1)
            new_dp1 = dp2 + prices[i]
            new_dp2 = max(dp2, dp0 - prices[i])
            dp0, dp1, dp2 = new_dp0, new_dp1, new_dp2

        return max(dp0, dp1)
```

**Tag: 数组、动态规划**

# 买卖股票的最佳时机

Link => [买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

## 题目
给定一个数组 prices ，它的第 i 个元素 prices[i] 表示一支给定股票第 i 天的价格。

你只能选择 某一天 买入这只股票，并选择在 未来的某一个不同的日子 卖出该股票。设计一个算法来计算你所能获取的最大利润。

返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 0 。

**示例1**
>输入：[7,1,5,3,6,4]<br />
>输出：5<br />
>解释：在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。<br />
>注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格；同时，你不能在买入前卖出股票。<br />

**示例2**
>输入：prices = [7,6,4,3,1]<br />
>输出：0<br />
>解释：在这种情况下, 没有交易完成, 所以最大利润为 0。<br />

执行结果：
通过
显示详情

添加备注
执行用时：76 ms, 在所有 Python3 提交中击败了99.95% 的用户
内存消耗：22.9 MB, 在所有 Python3 提交中击败了65.47% 的用户
通过测试用例：211 / 211

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        temp_min = inf
        temp_max = -inf
        res = []

        for price in prices:
            if price < temp_min:
                res.append(temp_max - temp_min)
                temp_min = price
                temp_max = price
            else:
                if price > temp_max:
                    temp_max = price

        res.append(temp_max - temp_min)

        return max(res)
```
改进：
省一点内存
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        temp_min = inf
        temp_max = -inf
        res = -inf

        for price in prices:
            if price < temp_min:
                res = max(res, temp_max - temp_min)
                temp_min = price
                temp_max = price
            else:
                if price > temp_max:
                    temp_max = price

        res = max(res, temp_max - temp_min)

        return res
```
**Tag: 贪心、数组、哈希表、计数、排序、堆（优先队列）**

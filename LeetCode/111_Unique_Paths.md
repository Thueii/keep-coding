# 不同路径

Link => [不同路径](https://leetcode-cn.com/problems/unique-paths/)

## 题目

    一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为 "Start" ）。

    机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 "Finish" ）。

    问总共有多少条不同的路径？

**示例1**

    输入：m = 3, n = 7
    输出：28

**执行结果：通过 显示详情**
确实感觉没什么技巧，写的很慢吧

- 执行用时：32 ms, 在所有 Python3 提交中击败了70.56% 的用户
内存消耗：15 MB, 在所有 Python3 提交中击败了51.72% 的用户
通过测试用例：62 / 62

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        return comb(m + n - 2, m - 1)
```

**Tag: 数学**

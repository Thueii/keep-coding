# 最小路径和

Link => [最小路径和](https://leetcode-cn.com/problems/minimum-path-sum/)

## 题目

    给定一个包含非负整数的 m x n 网格 grid ，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

    说明：每次只能向下或者向右移动一步。



**示例1**

    输入：grid = [[1,3,1],[1,5,1],[4,2,1]]
    输出：7
    解释：因为路径 1→3→1→1→1 的总和最小。

**示例2**

    输入：grid = [[1,2,3],[4,5,6]]
    输出：12

**执行结果：通过 显示详情**
全排列超时了

- 超时

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        max_y = len(grid[0]) - 1
        max_x = len(grid) - 1
        res = inf
        def dfs(cur, posx, posy):
            nonlocal res
            if posx == max_x and posy == max_y:
                print(cur)
                res = min(res, cur)
                return
            if posx + 1 <= max_x:
                dfs(cur + grid[posx + 1][posy], posx + 1, posy)
            if posy + 1 <= max_y:
                dfs(cur + grid[posx][posy + 1], posx, posy + 1)
        dfs(grid[0][0], 0, 0)
        return res
```
**改进**
就应该用动态规划的，看题目说了只能向右和向下就应该很敏感的选动态规划

- 执行用时：44 ms, 在所有 Python3 提交中击败了68.60% 的用户
内存消耗：16.4 MB, 在所有 Python3 提交中击败了47.45% 的用户
通过测试用例：61 / 61

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        max_y = len(grid[0])
        max_x = len(grid)
        dp = [[inf for i in range(max_y + 1)] for j in range(max_x + 1)]

        dp[0][1] = 0
        dp[1][0] = 0
        for i in range(1, max_x+1):
            for j in range(1, max_y+1):
                dp[i][j] = min(dp[i-1][j], dp[i][j-1]) + grid[i-1][j-1]
        return dp[-1][-1]
```
好像这题python只能写成这样
**Tag: 数组、排序**

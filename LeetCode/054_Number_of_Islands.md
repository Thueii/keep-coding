# 岛屿数量

Link => [岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)

## 题目
给你一个由 '1'（陆地）和 '0'（水）组成的的二维网格，请你计算网格中岛屿的数量。

岛屿总是被水包围，并且每座岛屿只能由水平方向和/或竖直方向上相邻的陆地连接形成。

此外，你可以假设该网格的四条边均被水包围。

**示例1**
>输入：grid = [<br />
  ["1","1","1","1","0"],<br />
  ["1","1","0","1","0"],<br />
  ["1","1","0","0","0"],<br />
  ["0","0","0","0","0"]<br />
]<br />
>输出：1<br />


**示例2**
>输入：grid = [<br />
  ["1","1","0","0","0"],<br />
  ["1","1","0","0","0"],<br />
  ["0","0","1","0","0"],<br />
  ["0","0","0","1","1"]<br />
]<br />
>输出：3<br />

**执行结果：通过 显示详情**
思路：深度优先算法，我其实不会写，看了题解说这个深度优先算法突然开窍开始写，居然两次就成功了，很高兴

- 执行用时：72 ms, 在所有 Python3 提交中击败了94.32% 的用户
内存消耗：23.7 MB, 在所有 Python3 提交中击败了32.21% 的用户
通过测试用例：49 / 49
```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        res = 0
        def dfs(i, j, grid):
            if (i-1) >= 0 and grid[i-1][j] == "1":
                grid[i-1][j] = "0"
                dfs(i-1, j, grid)
            if (i+1) < len(grid) and grid[i+1][j] == "1":
                grid[i+1][j] = "0"
                dfs(i+1, j, grid)
            if (j-1) >= 0 and grid[i][j-1] == "1":
                grid[i][j-1] = "0"
                dfs(i, j-1, grid)
            if (j+1) < len(grid[0]) and grid[i][j+1] == "1":
                grid[i][j+1] = "0"
                dfs(i, j+1, grid)
            return

        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == "1":
                    grid[i][j] = "0"
                    dfs(i, j, grid)
                    res += 1
        return res
```
**Tag: 深度优先搜索、广度优先搜索、并查集、数组、矩阵**

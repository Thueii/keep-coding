# 最大正方形

Link => [最大正方形](https://leetcode-cn.com/problems/maximal-square/)

## 题目

    在一个由 '0' 和 '1' 组成的二维矩阵内，找到只包含 '1' 的最大正方形，并返回其面积。

**执行结果：通过 显示详情**
常规方法，好慢啊

- 执行用时：152 ms, 在所有 Python3 提交中击败了22.43% 的用户
内存消耗：27.7 MB, 在所有 Python3 提交中击败了12.02% 的用户
通过测试用例：77 / 77

```python
class Solution:
    def maximalSquare(self, matrix: List[List[str]]) -> int:
        # dp[i][j]表示以i，j为下标的位置的最大正方形边长
        dp = [[0] * len(matrix[0]) for _ in range(len(matrix))]

        res_len = 0

        for i in range(len(dp)):
            for j in range(len(dp[0])):
                if matrix[i][j] == '1':
                    if j == 0:
                        dp[i][j] = 1
                    elif i == 0:
                        dp[i][j] = 1
                    else:
                        dp[i][j] = min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + 1
                        
                    res_len = max(res_len, dp[i][j])
        return res_len ** 2
```

**改进**
看不懂！！！！！！我是傻逼
自己去看吧。。。
**Tag: 数组、二分查找、动态规划**

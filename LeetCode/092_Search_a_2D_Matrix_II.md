# 搜索二维矩阵 II

Link => [搜索二维矩阵 II](https://leetcode-cn.com/problems/search-a-2d-matrix-ii/)

## 题目

    编写一个高效的算法来搜索 m x n 矩阵 matrix 中的一个目标值 target 。该矩阵具有以下特性：

    每行的元素从左到右升序排列。
    每列的元素从上到下升序排列。

**执行结果：通过 显示详情**
从右上角看其实是一个二分查找树，，要对题目敏感

- 执行用时：148 ms, 在所有 Python3 提交中击败了87.33% 的用户
内存消耗：20.9 MB, 在所有 Python3 提交中击败了90.06% 的用户
通过测试用例：129 / 129

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        max_r = len(matrix) - 1
        l, r = len(matrix[0]) - 1, 0
        while l >= 0 and r <= max_r:
            if matrix[r][l] == target:
                return True
            if matrix[r][l] > target:
                l -= 1
            else:
                r += 1
        return False
```

**Tag: 数组、二分查找、分治、矩阵**

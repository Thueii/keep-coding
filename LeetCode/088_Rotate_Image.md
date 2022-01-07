# 旋转图像

Link => [旋转图像](https://leetcode-cn.com/problems/rotate-image/)

## 题目

    给定一个 n × n 的二维矩阵 matrix 表示一个图像。请你将图像顺时针旋转 90 度。

    你必须在 原地 旋转图像，这意味着你需要直接修改输入的二维矩阵。请不要 使用另一个矩阵来旋转图像。


**示例1**

    输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
    输出：[[7,4,1],[8,5,2],[9,6,3]]


**示例2**

    输入：matrix = [[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]
    输出：[[15,13,2,5],[14,3,4,1],[12,6,8,9],[16,7,10,11]]

**执行结果：通过 显示详情**
主要是要明白怎么才是一个轮回，总不能一圈一圈的搞，因为太多了，可以四个四个，最方便！

- 执行用时：24 ms, 在所有 Python3 提交中击败了96.85% 的用户
内存消耗：14.8 MB, 在所有 Python3 提交中击败了92.45% 的用户
通过测试用例：21 / 21

```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        pos1, pos2 = 0, len(matrix) - 1
        while pos1 < pos2: # 一圈，做完缩一圈
            add = 0
            while add < pos2 - pos1: # 做一圈
                tmp = matrix[pos2 - add][pos1]
                matrix[pos2 - add][pos1] = matrix[pos2][pos2 - add]
                matrix[pos2][pos2 - add] = matrix[pos1 + add][pos2]
                matrix[pos1 + add][pos2] = matrix[pos1][pos1 + add]
                matrix[pos1][pos1 + add] = tmp

                add += 1
            pos1 += 1
            pos2 -= 1
```

**Tag: 数组、数学、矩阵**

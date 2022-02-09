# 二叉树的最小深度

Link => [二叉树的最小深度](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/)

## 题目

    给定一个二叉树，找出其最小深度。

    最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

    说明：叶子节点是指没有子节点的节点。

**示例1**

    输入：root = [3,9,20,null,null,15,7]
    输出：2

**示例2**

    输入：root = [2,null,3,null,4,null,5,null,6]
    输出：5

**执行结果：通过 显示详情**
常规

- 执行用时：436 ms, 在所有 Python3 提交中击败了66.81% 的用户
内存消耗：50.7 MB, 在所有 Python3 提交中击败了84.05% 的用户
通过测试用例：52 / 52

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def minDepth(self, root: TreeNode) -> int:
        if not root:
            return 0
        stack = [root]
        res = 0
        while stack:
            res += 1
            tmp = []
            for node in stack:
                if not node.left and not node.right:
                    return res
                if node.left:
                    tmp.append(node.left)
                if node.right:
                    tmp.append(node.right)
            stack = tmp
```
**Tag: 树、深度优先搜索、广度优先搜索、二叉树**

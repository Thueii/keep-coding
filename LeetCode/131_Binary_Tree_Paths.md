# 二叉树的所有路径

Link => [二叉树的所有路径](https://leetcode-cn.com/problems/binary-tree-paths/)

## 题目

    给你一个二叉树的根节点 root ，按 任意顺序 ，返回所有从根节点到叶子节点的路径。

    叶子节点 是指没有子节点的节点。

**执行结果：通过 显示详情**
简单

- 执行用时：32 ms, 在所有 Python3 提交中击败了77.58% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了7.59% 的用户
通过测试用例：208 / 208

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def binaryTreePaths(self, root: Optional[TreeNode]) -> List[str]:
        res = set()
        def dfs(root, now):
            if not root.left and not root.right:
                res.add(now)
                return
            if root.left:
                dfs(root.left, now+"->"+str(root.left.val))
            if root.right:
                dfs(root.right, now+"->"+str(root.right.val))
            return
        dfs(root, str(root.val))
        return list(res)
```
**Tag: 树、深度优先搜索、字符串、回溯、二叉树**

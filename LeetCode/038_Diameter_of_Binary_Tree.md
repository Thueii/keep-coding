# 二叉树的直径

Link => [二叉树的直径](https://leetcode-cn.com/problems/diameter-of-binary-tree/)

## 题目
给定一棵二叉树，你需要计算它的直径长度。一棵二叉树的直径长度是任意两个结点路径长度中的最大值。这条路径可能穿过也可能不穿过根结点。

**执行结果：通过 显示详情**

- 执行用时：36 ms, 在所有 Python3 提交中击败了93.62% 的用户
内存消耗：16.9 MB, 在所有 Python3 提交中击败了61.54% 的用户
通过测试用例：104 / 104

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def diameterOfBinaryTree(self, root: TreeNode) -> int:
        # 这个题不是单纯的计算两边的最大深度，而是每个节点都可能是那个“根节点”
        # 可能是那个点的左右两边加起来超过经过根节点的

        res = 0
        def dfs(root):
            nonlocal res
            # 计算当前树的最大深度
            if not root:
                return 0
            left = dfs(root.left)
            right = dfs(root.right)
            res = max(res, left + right)
            return max(left, right) + 1
        dfs(root)
        return res
```
**Tag: 树、深度优先搜索、二叉树**

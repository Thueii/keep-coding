# 合并二叉树

Link => [合并二叉树](https://leetcode-cn.com/problems/invert-binary-tree/)

## 题目
给定两个二叉树，想象当你将它们中的一个覆盖到另一个上时，两个二叉树的一些节点便会重叠。

你需要将他们合并为一个新的二叉树。合并的规则是如果两个节点重叠，那么将他们的值相加作为节点合并后的新值，否则不为 NULL 的节点将直接作为新二叉树的节点。

**执行结果：通过 显示详情**

- 执行用时：52 ms, 在所有 Python3 提交中击败了96.47% 的用户
内存消耗：15.2 MB, 在所有 Python3 提交中击败了86.28% 的用户
通过测试用例：182 / 182

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def mergeTrees(self, root1: TreeNode, root2: TreeNode) -> TreeNode:
        # 这题自己没想起来怎么做，楚哥直接跟我说五行，然后return，心伤了哈哈= =我太菜了

        if not (root1 and root2):
            return root1 if root1 else root2
        node = TreeNode(root1.val + root2.val)
        node.left = self.mergeTrees(root1.left, root2.left)
        node.right = self.mergeTrees(root1.right, root2.right)
        return node
```
**改进：**

- 可以直接在root1上做，减少空间使用
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def mergeTrees(self, root1: TreeNode, root2: TreeNode) -> TreeNode:
        if not (root1 and root2):
            return root1 if root1 else root2
        root1.val += root2.val
        root1.left = self.mergeTrees(root1.left, root2.left)
        root1.right = self.mergeTrees(root1.right, root2.right)
        return root1
```
**Tag: 树、深度优先搜索、广度优先搜索、二叉树**

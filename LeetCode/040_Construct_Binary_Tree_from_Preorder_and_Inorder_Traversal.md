# 把二叉搜索树转换为累加树

Link => [把二叉搜索树转换为累加树](https://leetcode-cn.com/problems/convert-bst-to-greater-tree/)

## 题目
给定一棵树的前序遍历 preorder 与中序遍历  inorder。请构造二叉树并返回其根节点。

**示例1**
>输入：preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]<br />
>输出：[3,9,20,null,null,15,7]<br />

**执行结果：通过 显示详情**

- 执行用时：168 ms, 在所有 Python3 提交中击败了19.98% 的用户
内存消耗：88 MB, 在所有 Python3 提交中击败了5.10% 的用户
通过测试用例：203 / 203

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        # 根, [左树前序], [右树前序]
        # [左树中序], 根, [右树中序]
        # 写的好菜好菜，但是好歹跑通了。。。还是高兴的
        def dfs(preorder, inorder):
            if len(preorder) == 1:
                return TreeNode(preorder[0])
            if not preorder:
                return None
            root = TreeNode(preorder[0])
            left_mid = inorder[0:inorder.index(preorder[0])]
            right_mid = inorder[inorder.index(preorder[0])+1::]
            left_pre = preorder[1:len(left_mid)+1]
            right_pre = preorder[len(left_pre)+1::]
            root.left = dfs(left_pre, left_mid)
            root.right = dfs(right_pre, right_mid)
            return root
        return dfs(preorder, inorder)
```
**改进：**

- 执行用时：132 ms, 在所有 Python3 提交中击败了52.71% 的用户
内存消耗：87 MB, 在所有 Python3 提交中击败了39.33% 的用户
通过测试用例：203 / 203
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        # 简化一下，思想是一样的，但是快一些，也省空间
        if not preorder:
            return None
        root = TreeNode(preorder[0])
        separateIdx = inorder.index(root.val)
        root.left = self.buildTree(preorder[1:1 + separateIdx], inorder[:separateIdx])
        root.right = self.buildTree(preorder[1 + separateIdx:], inorder[separateIdx + 1:])
        return root
```
**Tag: 树、深度优先搜索、二叉树**

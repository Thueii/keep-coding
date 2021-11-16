# 翻转二叉树

Link => [翻转二叉树](https://leetcode-cn.com/problems/invert-binary-tree/)

## 题目
翻转一棵二叉树。

**执行结果：通过 显示详情**

- 执行用时：36 ms, 在所有 Python3 提交中击败了34.73% 的用户
内存消耗：14.9 MB, 在所有 Python3 提交中击败了69.78% 的用户
通过测试用例：77 / 77

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:
        # 递归做感觉总是很慢
        # 想一想用迭代呢

        if not root:
            return root

        def dfs(root):
            if not root:
                return None
            if not root.left and not root.right:
                return root
            root.left, root.right = dfs(root.right), dfs(root.left)
            return root
        return dfs(root)
```
**改进：**

- 还是迭代比较快，注意迭代的话最重要的是要有个一个栈，这也是空间换时间吧，反复的pop来记录之前的状态，快很多

- 执行结果：
通过
显示详情

- 添加备注
执行用时：32 ms, 在所有 Python3 提交中击败了64.94% 的用户
内存消耗：14.7 MB, 在所有 Python3 提交中击败了97.74% 的用户
通过测试用例：77 / 77

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:
        if not root:
            return root
        # 迭代的精髓，就是搞个栈

        stack = [root]
        while stack:
            temp = stack.pop()
            temp.left, temp.right = temp.right, temp.left
            if temp.left:
                stack.append(temp.left)
            if temp.right:
                stack.append(temp.right)
        return root
```
**Tag: 树、深度优先搜索、广度优先搜索、二叉树**

# 对称二叉树

Link => [对称二叉树](https://leetcode-cn.com/problems/symmetric-tree/)

## 题目
给定一个二叉树，检查它是否是镜像对称的。

**示例1**
>输入：[1,2,2,3,4,4,3]<br />
>输出：true<br />

**示例2**
>输入：[1,2,2,null,3,null,3] <br />
>输出：false<br />

**执行结果：通过 显示详情**

- 执行用时：36 ms, 在所有 Python3 提交中击败了56.39% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了43.03% 的用户
通过测试用例：197 / 197

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        # 写的太差了
        # 遍历两次，左右各一次，判断是否对称

        head = root
        left_list = []
        val_list = []
        while left_list or root:
            while root:
                val_list.append(root.val)
                left_list.append(root)
                root = root.left
            root = left_list.pop()
            if root.right and not root.left:
                val_list.append("F")
            if root.left and not root.right:
                val_list.append("F")
            root = root.right
        
        root = head
        left_list2 = []
        val_list2 = []
        while left_list2 or root:
            while root:
                val_list2.append(root.val)
                left_list2.append(root)
                root = root.right
            root = left_list2.pop()
            if root.left and not root.right:
                val_list2.append("F")
            if root.right and not root.left:
                val_list2.append("F")
            root = root.left

        return val_list2 == val_list
```
**改进：**

- 其实不可能要遍历两遍完成，要是一遍完成就必要两遍对比，所以有了下面的递归办法

- 执行结果：
通过
显示详情

- 添加备注
执行用时：36 ms, 在所有 Python3 提交中击败了56.39% 的用户
内存消耗：15 MB, 在所有 Python3 提交中击败了66.45% 的用户
通过测试用例：197 / 197

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        def dfs(left_tree, right_tree):
            # 判断左右两边是否相等，注意要用左树的左边和右树的右边比
            # 以及左树的右边和右树的左边比较
            # 虽然挺好的，中途就能发现错误，但是递归是很慢的

            if not left_tree and not right_tree:
                return True
            elif not left_tree or not right_tree:
                return False
            elif left_tree.val != right_tree.val:
                return False
            else:
                return dfs(left_tree.left, right_tree.right) and dfs(left_tree.right, right_tree.left)
        return dfs(root.left, root.right)
```
**改进：**

- 还是迭代比较快，注意迭代的话最重要的是要有个一个栈，这也是空间换时间吧，反复的pop来记录之前的状态，快很多

- 执行结果：
通过
显示详情

- 添加备注
执行用时：28 ms, 在所有 Python3 提交中击败了93.94% 的用户
内存消耗：15 MB, 在所有 Python3 提交中击败了68.18% 的用户
通过测试用例：197 / 197

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        # 思想就是每个root都判断一下，再放进去下一层root，再判断，再放下一层

        if not root:
            return True
        stack = [root.left, root.right]
        while stack:
            left = stack.pop()
            right = stack.pop()
            if not left and not right:
                continue
            if not left or not right:
                return False
            if left.val != right.val:
                return False
            stack.append(left.left)
            stack.append(right.right)
            stack.append(left.right)
            stack.append(right.left)
        return True
```
**Tag: 树、深度优先搜索、广度优先搜索、二叉树**

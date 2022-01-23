# 二叉树展开为链表

Link => [二叉树展开为链表](https://leetcode-cn.com/problems/flatten-binary-tree-to-linked-list/)

给你二叉树的根结点 root ，请你将它展开为一个单链表：

    展开后的单链表应该同样使用 TreeNode ，其中 right 子指针指向链表中下一个结点，而左子指针始终为 null 。
    展开后的单链表应该与二叉树 先序遍历 顺序相同。

>输入：root = [1,2,5,3,4,null,6]<br />
>输出：[1,null,2,null,3,null,4,null,5,null,6]<br />

执行结果：
通过
显示详情

添加备注
执行用时：32 ms, 在所有 Python3 提交中击败了86.08% 的用户
内存消耗：15.4 MB, 在所有 Python3 提交中击败了5.06% 的用户
通过测试用例：225 / 225

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def flatten(self, root: TreeNode) -> None:
        """
        Do not return anything, modify root in-place instead.
        """
        if root is None:
            return []

        def dfs(root):
            if root is None:
                return []
            return [root.val] + dfs(root.left) + dfs(root.right)

        new_list = dfs(root)
        p = root
        for i in range(len(new_list)):
            if i == 0:
                p.val = new_list[i]
                p.left = None
            else:
                r_p = TreeNode(new_list[i])
                p.right = r_p
                p = p.right
```
改进：
执行结果：
通过
显示详情

添加备注
执行用时：28 ms, 在所有 Python3 提交中击败了96.58% 的用户
内存消耗：14.7 MB, 在所有 Python3 提交中击败了97.74% 的用户
通过测试用例：225 / 225

需要画图
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def flatten(self, root):
        while root:
            if root.left:
                temp = root.left
                while temp.right:
                    temp = temp.right
                temp.right = root.right
                root.right = root.left
                root.left = None
            root = root.right
```
**2022/01/23**
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def flatten(self, root: TreeNode) -> None:
        """
        Do not return anything, modify root in-place instead.
        """
        cur = root
        while cur:
            if cur.left:
                left_p = cur.left
                while left_p.right:
                    left_p = left_p.right
                left_p.right = cur.right
                cur.right = cur.left
                cur.left = None
            cur = cur.right
        return root
```
**Tag: 栈、树、深度优先搜索、链表、二叉树**

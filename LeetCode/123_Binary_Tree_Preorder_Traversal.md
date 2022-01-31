# 二叉树的前序遍历

Link => [二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)

## 题目

    给你二叉树的根节点 root ，返回它节点值的 前序 遍历。

**示例1**

    输入：root = [1,null,2,3]
    输出：[1,2,3]

**示例2**

    输入：root = []
    输出：[]


**执行结果：通过 显示详情**
迭代

- 执行用时：28 ms, 在所有 Python3 提交中击败了88.53% 的用户
内存消耗：15 MB, 在所有 Python3 提交中击败了44.28% 的用户
通过测试用例：69 / 69

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []
        res = []
        stack = [root]
        while stack:
            tmp = stack.pop()
            res.append(tmp.val)
            if tmp.right:
                stack.append(tmp.right)
            if tmp.left:
                stack.append(tmp.left)
        return res
```
**方法2**
递归

- 执行用时：36 ms, 在所有 Python3 提交中击败了34.94% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了7.74% 的用户
通过测试用例：69 / 69

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res = []
        def dfs(root):
            if not root:
                return
            res.append(root.val)
            dfs(root.left)
            dfs(root.right)
        dfs(root)
        return res

```
**Tag: 栈、树、深度优先搜索、二叉树**

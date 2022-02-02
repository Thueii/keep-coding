# 相同的树

Link => [相同的树](https://leetcode-cn.com/problems/same-tree/)

**题目**

    给你两棵二叉树的根节点 p 和 q ，编写一个函数来检验这两棵树是否相同。

    如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

**示例1**

    输入：p = [1,2,3], q = [1,2,3]
    输出：true

**示例 2**

    输入：p = [1,2], q = [1,null,2]
    输出：false

**示例 3**

    输入：p = [1,2,1], q = [1,1,2]
    输出：false

**结果**
递归 很好想

- 执行用时：36 ms, 在所有 Python3 提交中击败了38.42% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了28.48% 的用户
通过测试用例：60 / 60

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        def dfs(p, q):
            if not p and not q:
                return True
            if not p or not q:
                return False
            if p.val != q.val:
                return False
            return dfs(p.left, q.left) and dfs(p.right, q.right)
        return dfs(p, q)
```
**Tag: 树、广度优先搜索、二叉树**

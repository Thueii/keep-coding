# 二叉树的中序遍历

Link => [ 二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)

给定一个二叉树的根节点 root ，返回它的 中序 遍历。

>输入：root = [1,null,2,3]<br />
>输出：[1,3,2]<br />

执行结果：
通过
显示详情

添加备注
执行用时：24 ms, 在所有 Python3 提交中击败了96.81% 的用户
内存消耗：15 MB, 在所有 Python3 提交中击败了46.88% 的用户
通过测试用例：68 / 68

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        def dfs(root):
            if root is None:
                return
            dfs(root.left)
            res.append(root.val)
            dfs(root.right)
        dfs(root)
        return res
```

**Tag: 栈、树、深度优先搜索、二叉树**

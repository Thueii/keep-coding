# 路径总和

Link => [路径总和](https://leetcode-cn.com/problems/path-sum/)

## 题目

    给你二叉树的根节点 root 和一个表示目标和的整数 targetSum 。判断该树中是否存在 根节点到叶子节点 的路径，这条路径上所有节点值相加等于目标和 targetSum 。如果存在，返回 true ；否则，返回 false 。

    叶子节点 是指没有子节点的节点。

**示例1**

    输入：root = [5,4,8,11,null,13,4,7,2,null,null,null,1], targetSum = 22
    输出：true
    解释：等于目标和的根节点到叶节点路径如上图所示。

**示例2**

    输入：root = [], targetSum = 0
    输出：false
    解释：由于树是空的，所以不存在根节点到叶子节点的路径。

**执行结果：通过 显示详情**
回溯

- 执行用时：40 ms, 在所有 Python3 提交中击败了80.60% 的用户
内存消耗：16.3 MB, 在所有 Python3 提交中击败了5.15% 的用户
通过测试用例：117 / 117

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        if not root:
            return False

        def dfs(root, target):
            if not root:
                return False
            if not root.left and not root.right:
                return target == root.val
            return dfs(root.left, target-root.val) or dfs(root.right, target-root.val)
        return dfs(root, targetSum)
```
**其他**
迭代

- 执行用时：44 ms, 在所有 Python3 提交中击败了55.97% 的用户
内存消耗：16.1 MB, 在所有 Python3 提交中击败了6.78% 的用户
通过测试用例：117 / 117
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        if not root:
            return False
        q = deque()
        q.append((root, targetSum))
        while q:
            root, tar = q.popleft()
            if not root.left and not root.right:
                if tar == root.val:
                    return True
            if root.left:
                q.append((root.left, tar-root.val))
            if root.right:
                q.append((root.right, tar-root.val))
        return False
```
**Tag: 树、深度优先搜索、广度优先搜索、二叉树**

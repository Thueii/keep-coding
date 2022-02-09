# 路径总和 II

Link => [路径总和 II](https://leetcode-cn.com/problems/path-sum-ii/)

## 题目

    给你二叉树的根节点 root 和一个整数目标和 targetSum ，找出所有 从根节点到叶子节点 路径总和等于给定目标和的路径。

    叶子节点 是指没有子节点的节点。

**示例1**

    输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
    输出：[[5,4,11,2],[5,8,4,5]]

**示例2**

    输入：root = [1,2,3], targetSum = 5
    输出：[]

**执行结果：通过 显示详情**
回溯

- 执行用时：52 ms, 在所有 Python3 提交中击败了23.45% 的用户
内存消耗：20.3 MB, 在所有 Python3 提交中击败了8.81% 的用户
通过测试用例：115 / 115

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
        res = []
        def dfs(root, now, tar):
            if not root:
                return
            if not root.left and not root.right:
                if tar == root.val:
                    res.append(now+[root.val])
                return
            dfs(root.left, now+[root.val], tar-root.val)
            dfs(root.right, now+[root.val], tar-root.val)
        dfs(root, [], targetSum)
        return res
```
**迭代来一个**
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
        res = []
        q = deque()
        q.append((root, targetSum, []))
        while q:
            tmp, tar, now = q.popleft()
            if not tmp:
                continue
            if not tmp.left and not tmp.right:
                if tar == tmp.val:
                    res.append(now+[tmp.val])
                continue
            q.append((tmp.left, tar-tmp.val, now+[tmp.val]))
            q.append((tmp.right, tar-tmp.val, now+[tmp.val]))
        return res
```
**Tag: 树、深度优先搜索、回溯、二叉树**

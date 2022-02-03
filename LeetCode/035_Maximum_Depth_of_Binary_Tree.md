# 二叉树的最大深度

Link => [二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)

## 题目
给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

**示例1**
>输入：[3,9,20,null,null,15,7]<br />
>输出：3<br />

**执行结果：通过 显示详情**

- 执行用时：36 ms, 在所有 Python3 提交中击败了87.04% 的用户
内存消耗：15.9 MB, 在所有 Python3 提交中击败了93.02% 的用户
通过测试用例：39 / 39

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        count = 0
        if not root:
            return count
        root_list = [root]
        while root_list:
            count += 1
            temp_list = []
            for each in root_list:
                if each.left:
                    temp_list.append(each.left)
                if each.right:
                    temp_list.append(each.right)
            root_list = temp_list
        return count
```
**参考：**

- 一个dfs做法，找到左子树和右子树中最大的然后加1（表示当前的root节点）

- 执行结果：
通过
显示详情

- 添加备注
执行用时：44 ms, 在所有 Python3 提交中击败了39.59% 的用户
内存消耗：16.7 MB, 在所有 Python3 提交中击败了49.25% 的用户
通过测试用例：39 / 39

```python
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        # 速度慢，但是思考很重要

        if not root:
            return 0
        l = self.maxDepth(root.left)
        r = self.maxDepth(root.right)
        return max(l,r) + 1
```
**2022/02/03**
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        return max(self.maxDepth(root.left), self.maxDepth(root.right)) + 1
```
**Tag: 树、深度优先搜索、广度优先搜索、二叉树**

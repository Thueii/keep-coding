# 求根节点到叶节点数字之和

Link => [求根节点到叶节点数字之和](https://leetcode-cn.com/problems/sum-root-to-leaf-numbers/)

## 题目

    给你一个二叉树的根节点 root ，树中每个节点都存放有一个 0 到 9 之间的数字。

    每条从根节点到叶节点的路径都代表一个数字：

**示例1**

    输入：root = [1,2,3]
    输出：25
    解释：
    从根到叶子节点路径 1->2 代表数字 12
    从根到叶子节点路径 1->3 代表数字 13
    因此，数字总和 = 12 + 13 = 25

**示例2**

    输入：root = [4,9,0,5,1]
    输出：1026
    解释：
    从根到叶子节点路径 4->9->5 代表数字 495
    从根到叶子节点路径 4->9->1 代表数字 491
    从根到叶子节点路径 4->0 代表数字 40
    因此，数字总和 = 495 + 491 + 40 = 1026

**执行结果：通过 显示详情**
回溯，注意两点，写在下面了

- 执行用时：32 ms, 在所有 Python3 提交中击败了71.22% 的用户
内存消耗：15 MB, 在所有 Python3 提交中击败了61.26% 的用户
通过测试用例：108 / 108

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sumNumbers(self, root: TreeNode) -> int:
        res = 0
        def get_sum(alist):
            res = 0
            for i in range(len(alist)):
                res = res*10 + alist[i] # 这里注意学习
            return res

        def dfs(root, now):
            nonlocal res
            if not root:
                return
            if not root.left and not root.right:
                res += get_sum(now+[root.val]) # 还有这里尽量边搞边加，不要最后用sum
                return
            dfs(root.left, now+[root.val])
            dfs(root.right, now+[root.val])
        dfs(root, [])
        return res
```
**Tag: 树、深度优先搜索、回溯、二叉树**

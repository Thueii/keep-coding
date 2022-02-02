# 二叉树的锯齿形层序遍历

Link => [二叉树的锯齿形层序遍历](https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal)

**题目**

    给你二叉树的根节点 root ，返回其节点值的 锯齿形层序遍历 。（即先从左往右，再从右往左进行下一层遍历，以此类推，层与层之间交替进行）。

**示例1**

    输入：root = [3,9,20,null,null,15,7]
    输出：[[3],[20,9],[15,7]]

**示例 2**

    输入：root = [1]
    输出：[[1]]

**示例 3**

    输入：root = []
    输出：[]

**结果**
一般思路，直接别绕了，统一从左往右，append的时候再[::-1]

- 执行用时：32 ms, 在所有 Python3 提交中击败了74.40% 的用户
内存消耗：15.2 MB, 在所有 Python3 提交中击败了75.10% 的用户
通过测试用例：33 / 33

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def zigzagLevelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root: return []
        res = []
        stack = [root]
        count = 0
        while stack:
            tmp = []
            tmp_res = []
            for node in stack:
                tmp_res.append(node.val)
                if node.left:
                    tmp.append(node.left)
                if node.right:
                    tmp.append(node.right)
            if count % 2:
                tmp_res = tmp_res[::-1]
            res.append(tmp_res)
            stack = tmp
            count += 1
        return res
```
**Tag: 树、广度优先搜索、二叉树**

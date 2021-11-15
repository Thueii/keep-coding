# 二叉树的层序遍历

Link => [二叉树的层序遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

## 题目
给你一个二叉树，请你返回其按 层序遍历 得到的节点值。 （即逐层地，从左到右访问所有节点）。

**示例1**
>输入：[3,9,20,null,null,15,7]<br />
>输出：[<br />
  [3],<br />
  [9,20],<br />
  [15,7]<br />
]<br />

**执行结果：通过 显示详情**

- 执行用时：32 ms, 在所有 Python3 提交中击败了72.89% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了95.99% 的用户
通过测试用例：34 / 34

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        # 把每一层都一次次的处理，然后从左到右遍历

        if not root:
            return []
        root_list = [root]
        res_list = []
        while root_list:
            res2 = []
            res_list2 = []
            for each in root_list:
                res_list2.append(each.val)
                if each.left:
                    res2.append(each.left)
                if each.right:
                    res2.append(each.right)
            res_list.append(res_list2)
            root_list = res2
        return res_list
```
**Tag: 树、广度优先搜索、二叉树**

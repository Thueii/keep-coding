# 把二叉搜索树转换为累加树

Link => [把二叉搜索树转换为累加树](https://leetcode-cn.com/problems/convert-bst-to-greater-tree/)

## 题目
给出二叉 搜索 树的根节点，该树的节点值各不相同，请你将其转换为累加树（Greater Sum Tree），使每个节点 node 的新值等于原树中大于或等于 node.val 的值之和。

提醒一下，二叉搜索树满足下列约束条件：

    节点的左子树仅包含键 小于 节点键的节点。
    节点的右子树仅包含键 大于 节点键的节点。
    左右子树也必须是二叉搜索树。

**执行结果：通过 显示详情**

- 执行用时：352 ms, 在所有 Python3 提交中击败了5.53% 的用户
内存消耗：17.7 MB, 在所有 Python3 提交中击败了5.06% 的用户
通过测试用例：215 / 215

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def convertBST(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        # 非常low的跑通了
        # 这里先跑一遍后序
        # 再跑一遍记录每个节点应该变成几
        # 再跑一次把值都变掉

        def dfs(root):
            if not root:
                return []
            return dfs(root.right) + [root.val] + dfs(root.left)

        def dfs2(root):
            if not root:
                return
            root.val = sum_list[order.index(root.val)]
            dfs2(root.left)
            dfs2(root.right)

        order = dfs(root)
        sum_list = []
        sum_num = 0
        for i in range(len(order)):
            sum_num += order[i]
            sum_list.append(sum_num)

        dfs2(root)
        return root

```
**Tag: 树、深度优先搜索、二叉树**

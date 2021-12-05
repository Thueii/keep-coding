# 打家劫舍 III

Link => [打家劫舍 III](https://leetcode-cn.com/problems/house-robber-iii/)

## 题目
在上次打劫完一条街道之后和一圈房屋后，小偷又发现了一个新的可行窃的地区。这个地区只有一个入口，我们称之为“根”。 除了“根”之外，每栋房子有且只有一个“父“房子与之相连。一番侦察之后，聪明的小偷意识到“这个地方的所有房屋的排列类似于一棵二叉树”。 如果两个直接相连的房子在同一天晚上被打劫，房屋将自动报警。

计算在不触动警报的情况下，小偷一晚能够盗取的最高金额。

**示例1**
>输入：[3,2,3,null,3,null,1]<br />
>输出：7 <br />

**示例2**
>输入：[3,4,5,1,3,null,1]<br />
>输出：9<br />

**执行结果：通过 显示详情**
直接看答案的，说实话看到打家劫舍就害怕，这种试一下再放回去的操作总是想不好
但是理解之后自己一下写出来了，还可以，希望下次遇到直接会写

- 执行用时：40 ms, 在所有 Python3 提交中击败了92.66% 的用户
内存消耗：16.9 MB, 在所有 Python3 提交中击败了53.41% 的用户
通过测试用例：124 / 124
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def rob(self, root: TreeNode) -> int:
        def rob_or_not_rob(root): # 返回当前节点偷或不偷能得到的最大结果
            if not root:
                return 0, 0
            left = rob_or_not_rob(root.left)
            right = rob_or_not_rob(root.right)
            rob = root.val + left[1] + right[1] # 选当前节点，则两边的不能选
            not_rob = max(left) + max(right) # 不选当前节点则可以选两边的（两边的也可以选或者不选）
            return rob, not_rob
        return max(rob_or_not_rob(root)) # 返回偷或者不偷当前节点的最大值
```
**Tag: 数、深度优先搜索、动态规划、二叉树**

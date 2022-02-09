# 二叉树最大宽度

Link => [二叉树最大宽度](https://leetcode-cn.com/problems/maximum-width-of-binary-tree/)

## 题目

    给定一个二叉树，编写一个函数来获取这个树的最大宽度。树的宽度是所有层中的最大宽度。这个二叉树与满二叉树（full binary tree）结构相同，但一些节点为空。

    每一层的宽度被定义为两个端点（该层最左和最右的非空节点，两端点间的null节点也计入长度）之间的长度。

**示例 1**

    输入: 

           1
         /   \
        3     2
       / \     \  
      5   3     9 

    输出: 4
    解释: 最大值出现在树的第 3 层，宽度为 4 (5,3,null,9)。


**执行结果：通过 显示详情**
如果结果和节点的值没有关系就一定要注意了，注意用索引的思想

- 执行用时：44 ms, 在所有 Python3 提交中击败了68.52% 的用户
内存消耗：15.9 MB, 在所有 Python3 提交中击败了41.36% 的用户
通过测试用例：112 / 112

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def widthOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        res = 1
        stack = [(0, root)]
        while stack:
            tmp = []
            for idx, root in stack:
                if root.left:
                    tmp.append((2*idx, root.left))
                if root.right:
                    tmp.append((2*idx+1, root.right))
            if not tmp:
                return res
            res = max(res, tmp[-1][0]- tmp[0][0] + 1)
            stack = tmp
```
**Tag: 树、深度优先搜索、广度优先搜索、二叉树**

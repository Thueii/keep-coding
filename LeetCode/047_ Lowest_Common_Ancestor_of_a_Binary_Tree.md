# 二叉树的最近公共祖先

Link => [二叉树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)

## 题目
给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个节点 p、q，最近公共祖先表示为一个节点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

**示例1**
>输入：root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1<br />
>输出：6<br />
>说明：最优路径是 2 -> 1 -> 3 ，路径和为 2 + 1 + 3 = 6<br />

**示例2**
>输入：root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4<br />
>输出：5<br />
>说明：节点 5 和节点 4 的最近公共祖先是节点 5 。因为根据定义最近公共祖先节点可以为节点本身。<br />

**执行结果：通过 显示详情**
写的是对的，但是无法通过，太慢了
我的思路是根据定义来的：祖先的定义： 若节点 ppp 在节点 rootrootroot 的左（右）子树中，或 p=rootp = rootp=root ，则称 rootrootroot 是 ppp 的祖先。

最近公共祖先的定义： 设节点 rootrootroot 为节点 p,qp, qp,q 的某公共祖先，若其左子节点 root.leftroot.leftroot.left 和右子节点 root.rightroot.rightroot.right 都不是 p,qp,qp,q 的公共祖先，则称 rootrootroot 是 “最近的公共祖先” 。

- 超出时间限制
显示详情

添加备注
最后执行的输入：
[-1,0,null,1,null,2,null,3,null,4,null,5,null,6,null,7,null,8,null,9,null,10,null,11,null,12,null,13,null,14,null,15,null,16,null,17,null,18,null,19,null,20,null,21,null,22,null,23,null,24,null,25,null,26,null,27,null,28,null,29,null,30,null,31,null,32,null,33,null,34,null,35,null,36,null,37,null,38,null,39,null,40,null,41,null,42,null,43,null,44,null,45,null,46,null,47,null,48,null,49,null,50,null,51,null,52,null,53,null,54,null,55,null,56,null,57,null,58,null,59,null,60,null,61,null,62,null,63,null,64,null,65,null,66,null,67,null,68,null,69,null,70,null,71,null,72,null,73,null,74,null,75,null,76,null,77,null,78,null,79,null,80,null,81,null,82,null,83,null,84,null,85,null,86,null,87,null,88,null,89,null,90,null,91,null,92,null,93,null,94,null,95,null,96,null,97,null,98,null,99,null,100,null,101,null,102,null,103,null,104,null,105,null,106,null,107,null,108,null,109,null,110,null,111,null,112,null,113,null,114,null,115,null,116,null,117,null,118,null,119,null,120,null,121,null,122,null 9998 9999
查看全部

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        def dfs(root, p):
            if not root:
                return False
            if p == root:
                return True
            else:
                if dfs(root.left, p) or dfs(root.right, p):
                    return True
                else:
                    return False
        def func(root):
            if not root:
                return False
            if dfs(root, p) and dfs(root, q) and (not(dfs(root.left, p) and dfs(root.left, q)) and not(dfs(root.right, p) and dfs(root.right, q))):
                return root
            else:
                return False
        tmp = [root]
        while tmp:
            root = tmp.pop()
            res = func(root)
            if res:
                return res
            if root.right:
                tmp.append(root.right)
            if root.left:
                tmp.append(root.left)
```
**改进：**
还是敢想，直接想，想一层，当前函数就干这个事儿，如果能在左边找到就在左边，右边就右边，都有就是root

- 执行用时：52 ms, 在所有 Python3 提交中击败了97.47% 的用户
内存消耗：25.7 MB, 在所有 Python3 提交中击败了47.67% 的用户
通过测试用例：31 / 31
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        # 此函数为找到最近的公共节点
        if not root:
            return 
        if p == root or q == root:
            return root
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        if left and right:
            return root
        elif left:
            return left
        elif right:
            return right
```
**Tag: 树、深度优先搜索、二叉树**

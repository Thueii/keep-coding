# 二叉树中的最大路径和

Link => [二叉树中的最大路径和](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/)

## 题目
路径 被定义为一条从树中任意节点出发，沿父节点-子节点连接，达到任意节点的序列。同一个节点在一条路径序列中 至多出现一次 。该路径 至少包含一个 节点，且不一定经过根节点。

路径和 是路径中各节点值的总和。

给你一个二叉树的根节点 root ，返回其 最大路径和 。

**示例1**
>输入：root = [1,2,3]<br />
>输出：6<br />
>说明：最优路径是 2 -> 1 -> 3 ，路径和为 2 + 1 + 3 = 6<br />

**示例2**
>输入：root = [-10,9,20,null,null,15,7]<br />
>输出：42<br />
>说明：最优路径是 15 -> 20 -> 7 ，路径和为 15 + 20 + 7 = 42<br />

**执行结果：通过 显示详情**
有一个解析很精髓：
(https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/solution/124di-gui-de-jing-sui-ji-lu-yi-xia-by-821218213/)
首先想到的是，我可以很容易的用递归计算二叉树所有节点的和，而在本题中，就需要比较路径的大小来设计递归。
其实二叉树的递归遍历，只要包含如下代码，就可以了，而针对不同的题目，
我们会设置一些递归的返回值（包括终止条件），设计递归函数的参数，或者用外部变量记录的方式，来达到题目的要求。
```python
def dfs(root):
    if not root: return
    dfs(root.left)
    dfs(root.right)
```
而返回值、参数、外部变量是不影响递归的进行的（只要有以上代码），这时候就是发挥人类智慧，开始设计递归的时候。
至少对于二叉树的递归，每个题目都可以这么想。

注意递归一定只要想一层你要怎么做

- 执行用时：72 ms, 在所有 Python3 提交中击败了84.84% 的用户
内存消耗：22.5 MB, 在所有 Python3 提交中击败了15.36% 的用户
通过测试用例：94 / 94

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        # 好像懂了一点
        self.path_sum = -inf
        def dfs(root):
            if not root:
                return 0
            left = dfs(root.left)
            right = dfs(root.right)
            # 记录sum是可以从左到右的
            self.path_sum = max(root.val + left + right, self.path_sum)
            # 但是作为子节点选路径是不能分叉的
            return max(0, max(right, left) + root.val)
        dfs(root)
        return self.path_sum

```
**2022/02/09**
```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
var path int

func max(n, m int) int {
    if n > m {
        return n
    }
    return m
}
func dfs(root *TreeNode) int {
    if root == nil {
        return 0
    }
    left := dfs(root.Left)
    right := dfs(root.Right)
    path = max(path, root.Val + left + right)

    return max(root.Val + max(left, right), 0)
}

func maxPathSum(root *TreeNode) int {
    path = math.MinInt32
    dfs(root)
    return path
}
```
**Tag: 树、深度优先搜索、动态规划、二叉树**

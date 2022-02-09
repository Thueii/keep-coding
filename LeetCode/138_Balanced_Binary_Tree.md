# 平衡二叉树

Link => [平衡二叉树](https://leetcode-cn.com/problems/balanced-binary-tree/)

## 题目

    给定一个二叉树，判断它是否是高度平衡的二叉树。

    本题中，一棵高度平衡二叉树定义为：

    一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1 。


**示例 1**

    输入：root = [3,9,20,null,null,15,7]
    输出：true

**示例 2**

    输入：root = [1,2,2,3,3,null,null,4,4]
    输出：false

**执行结果：通过 显示详情**
就是自底向上

- 执行用时：4 ms, 在所有 Go 提交中击败了95.53% 的用户
内存消耗：5.5 MB, 在所有 Go 提交中击败了98.77% 的用户
通过测试用例：228 / 228

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func max (n1 int, n2 int) int {
    if n1 > n2 {
        return n1
    }
    return n2
}

func abs (n int) int {
    if n >= 0 {
        return n
    }
    return n * (-1)
}

func height(root *TreeNode) int {
    if root == nil{
        return 0
    }
    Left := height(root.Left)
    Right := height(root.Right)
    if Left  == -1 || Right == -1 || abs(Left-Right) > 1 {
        return -1
    }
    return max(Left, Right) + 1
}

func isBalanced(root *TreeNode) bool {
    return height(root) >= 0
}
```
**Tag: 树、深度优先搜索、二叉树**

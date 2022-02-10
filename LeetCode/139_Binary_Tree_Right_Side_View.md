# 二叉树的右视图

Link => [二叉树的右视图](https://leetcode-cn.com/problems/binary-tree-right-side-view/)

## 题目
给定一个二叉树的 根节点 root，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。

**示例1**

    输入: [1,2,3,null,5,null,4]
    输出: [1,3,4]

**示例2**

    输入: [1,null,3]
    输出: [1,3]

**执行结果：通过 显示详情**
golang真的快。。。

- 执行用时：0 ms, 在所有 Go 提交中击败了100.00% 的用户
内存消耗：2.1 MB, 在所有 Go 提交中击败了99.57% 的用户
通过测试用例：215 / 215
```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func rightSideView(root *TreeNode) []int {
    res := []int{}
    if root == nil {
        return res
    }
    res = []int{root.Val}
    stack := []*TreeNode{root}
    for len(stack) != 0 {
        tmp := []*TreeNode{}
        for _, cur := range stack{
            if cur.Left != nil {
                tmp = append(tmp, cur.Left)
            }
            if cur.Right != nil {
                tmp = append(tmp, cur.Right)
            }
        }
        stack = tmp
        if len(stack) != 0 {
            res = append(res, stack[len(stack)-1].Val)
        }
    }
    return res
}
```
**Tag: 数、深度优先搜索、动态规划、二叉树**

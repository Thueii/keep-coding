# 二叉搜索树中的搜索

Link => [二叉搜索树中的搜索](https://leetcode-cn.com/problems/search-in-a-binary-search-tree/)

## 题目
给定二叉搜索树（BST）的根节点和一个值。 你需要在BST中找到节点值等于给定值的节点。 返回以该节点为根的子树。 如果节点不存在，则返回 NULL。
**示例1**
>输入：[4,2,7,1,3]<br />
>输出：2<br />


**执行结果：通过 显示详情**

- 执行用时：64 ms, 在所有 Python3 提交中击败了84.72% 的用户
内存消耗：16.9 MB, 在所有 Python3 提交中击败了61.69% 的用户
通过测试用例：36 / 36

```python
class Solution:
    def searchBST(self, root: TreeNode, val: int) -> TreeNode:
        if not root:
            return None

        stack = [root]
        while stack:
            root = stack.pop()
            if root.val == val:
                return root
            elif root.val < val and root.right:
                stack.append(root.right)
            elif root.val > val and root.left:
                stack.append(root.left)
            else:
                return None
        return None

```
**改进：**
递归写一个

- 执行用时：64 ms, 在所有 Python3 提交中击败了84.72% 的用户
内存消耗：17 MB, 在所有 Python3 提交中击败了9.38% 的用户
通过测试用例：36 / 36
```python
class Solution:
    def searchBST(self, root: TreeNode, val: int) -> TreeNode:
        if not root:
            return None

        if root.val == val:
            return root
        elif root.val < val:
            return self.searchBST(root.right, val)
        else:
            return self.searchBST(root.left, val)

```
**Tag: 树、二叉树、二叉树搜索树**

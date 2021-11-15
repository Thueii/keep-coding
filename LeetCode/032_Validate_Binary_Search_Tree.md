# 验证二叉搜索树

Link => [验证二叉搜索树](https://leetcode-cn.com/problems/validate-binary-search-tree/)

## 题目
给你一个二叉树的根节点 root ，判断其是否是一个有效的二叉搜索树。

有效 二叉搜索树定义如下：

    节点的左子树只包含 小于 当前节点的数。
    节点的右子树只包含 大于 当前节点的数。
    所有左子树和右子树自身必须也是二叉搜索树。

**示例1**
>输入：root = [2,1,3]<br />
>输出：true<br />

**示例2**
>输入：root = [5,1,4,null,null,3,6]<br />
>输出：false<br />
>解释：根节点的值是 5 ，但是右子节点的值是 4 。<br />

**执行结果：通过 显示详情**

- 执行用时：48 ms, 在所有 Python3 提交中击败了34.92% 的用户
内存消耗：17.2 MB, 在所有 Python3 提交中击败了84.25% 的用户
通过测试用例：80 / 80

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        # 深度查找，找到当前判断需要规定的左右范围
        # 但是好慢

        def dfs(root, left, right):
            if not root:
                return True
            return ((root.left.val if root.left else inf) > left) and ((root.left.val if root.left else -inf) < root.val) and ((root.right.val if root.right else -inf) < right) and (root.val < (root.right.val if root.right else inf)) and dfs(root.left, left, root.val) and dfs(root.right, root.val, right)
        return dfs(root, -inf, inf)
```
**改进：**

- 我写的有些乱，我判断了当前节点的下一个节点，其实只要判断当前节点就行了。。。
- 其实是一个意思，但是明确很多

- 执行结果：
通过
显示详情

- 添加备注
执行用时：40 ms, 在所有 Python3 提交中击败了82.87% 的用户
内存消耗：17.2 MB, 在所有 Python3 提交中击败了88.30% 的用户
通过测试用例：80 / 80

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        def dfs(root, left, right):
            if not root:
                return True
            if left < root.val < right:
                return dfs(root.left, left, root.val) and dfs(root.right, root.val, right)
            else:
                return False
        return dfs(root, -inf, inf)

```
**改进：**

- 中序遍历是一个递增的数组，注意中序遍历用while是怎么找的！！！没有写过，第一次写

- 执行结果：
通过
显示详情

- 添加备注
执行用时：40 ms, 在所有 Python3 提交中击败了82.87% 的用户
内存消耗：17.4 MB, 在所有 Python3 提交中击败了42.16% 的用户
通过测试用例：80 / 80

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        # 记录一个最小的值，然后用栈的形式可以往上找！！！这个之前也没有想到
        # 这样就可以往上比较

        stack = []
        pre = -inf
        while stack or root:
            while root:
                stack.append(root)
                root = root.left
            root = stack.pop()
            if root.val <= pre:
                return False
            pre = root.val
            root = root.right
        return True

```
**Tag: 树、深度优先搜索、二叉树、二叉搜索树**

# 路径总和 III

Link => [路径总和 III](https://leetcode-cn.com/problems/path-sum-iii/)

## 题目
给定一个二叉树的根节点 root ，和一个整数 targetSum ，求该二叉树里节点值之和等于 targetSum 的 路径 的数目。

路径 不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。

**示例1**
>输入：root = [10,5,-3,3,2,null,11,3,-2,null,1], targetSum = 8<br />
>输出：3<br />
>说明：和等于 8 的路径有 3 条，如图所示<br />

**示例2**
>输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22<br />
>输出：3<br />

**执行结果：通过 显示详情**
我的做法是所有的有找一遍，全部，太烂了

- 执行用时：1924 ms, 在所有 Python3 提交中击败了5.03% 的用户
内存消耗：16.3 MB, 在所有 Python3 提交中击败了54.04% 的用户
通过测试用例：126 / 126
```python
class Solution:
    def pathSum(self, root: TreeNode, targetSum: int) -> int:
        res = 0 # 全部满足的次数

        def _pathSum(root, targetSum, last_flag, flag): # 经历一遍
            nonlocal res
            if not root:
                return
            print(root.val, targetSum)
            
            if (targetSum - root.val) == 0:
                print(root.val)
                res += 1

            if flag: # 表示上一把如果选了现在就只能选
                _pathSum(root.left, targetSum-root.val, True, True)
                _pathSum(root.right, targetSum-root.val, True, True)

            else: # 表示上一把没有选的话，这一把选不选都行
                _pathSum(root.left, targetSum-root.val, False, True)
                _pathSum(root.right, targetSum-root.val, False, True)
                _pathSum(root.left, targetSum, False, False)
                _pathSum(root.right, targetSum, False, False)
        _pathSum(root, targetSum, False, False)
        return res
```
**执行结果：通过 显示详情**
看了一个小时的题解，终于看懂了，前缀和和恢复状态，主要是恢复状态这里一直没有懂

- 执行用时：44 ms, 在所有 Python3 提交中击败了91.49% 的用户
内存消耗：16.2 MB, 在所有 Python3 提交中击败了67.47% 的用户
通过测试用例：126 / 126

```python
class Solution:
    def pathSum(self, root: TreeNode, targetSum: int) -> int:
        # 做前序遍历同时记录该路径上的出现的次数，遍历完该路径后再恢复状态
        # 恢复状态的意思是回复当前的被加上的pre，因为接下来还要做其他路径的
        # 所以该路径的都要恢复
        # 每次程序哦度是做完一条路径才做别的路径的
        adict = collections.defaultdict(int)
        adict[0] = 1 # 哨兵
        pre = 0
        res = 0
        def pre_order(root):
            nonlocal adict, pre, res, targetSum
            if not root:
                return
            pre += root.val
            res += adict[pre - targetSum]
            adict[pre] += 1

            pre_order(root.left)
            pre_order(root.right)

            adict[pre] -= 1 # 恢复
            pre -= root.val # 恢复
        pre_order(root)
        return res
```
**Tag: 数、深度优先搜索、二叉树**

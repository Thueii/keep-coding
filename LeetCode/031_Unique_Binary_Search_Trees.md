# 不同的二叉搜索树  

Link => [不同的二叉搜索树](https://leetcode-cn.com/problems/unique-binary-search-trees/)

## 题目
给你一个整数 n ，求恰由 n 个节点组成且节点值从 1 到 n 互不相同的 二叉搜索树 有多少种？返回满足题意的二叉搜索树的种数。

**示例1**
>输入：n = 3<br />
>输出：5<br />

**示例2**
>输入：n = 1<br />
>输出：1<br />

**执行结果：通过 显示详情**

- 执行用时：28 ms, 在所有 Python3 提交中击败了86.13% 的用户
内存消耗：14.9 MB, 在所有 Python3 提交中击败了60.77% 的用户
通过测试用例：19 / 19

```python
class Solution:
    def numTrees(self, n: int) -> int:
        # 记录算过的东西
        # 复用来减少计算次数
        # 有动态规划那味儿

        adict = {}
        def dfs(n):
            if n == 0:
                return 1
            elif n == 1:
                return 1
            else:
                res = 0
                for each in range(1, n+1):
                    x = adict.get(each - 1) if adict.get(each - 1) else dfs(each - 1)
                    y = adict.get(n - each) if adict.get(n - each) else dfs(n - each)
                    res += x * y
                    if not adict.get(each - 1):
                        adict[each - 1] = x
                    if not adict.get(n - each):
                        adict[n - each] = y
                return res
        if n == 1:
            return 1
        else:
            return dfs(n)
```

**Tag: 树、二叉搜索树、数学、动态规划、二叉树**

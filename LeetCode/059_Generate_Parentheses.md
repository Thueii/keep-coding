# 括号生成

Link => [括号生成](https://leetcode-cn.com/problems/generate-parentheses/)

## 题目
数字 n 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 有效的 括号组合。

**示例1**
>输入：n = 3<br />
>输出：["((()))","(()())","(())()","()(())","()()()"]<br />


**执行结果：通过 显示详情**
深度优先搜索，看似很难但是要想明白：
1. 剩余右括号不能比左括号少
2. 由于给你的是几对，所以左右括号数量是一致的，只要在保证1的情况下把其余的填充就好了

- 执行用时：32 ms, 在所有 Python3 提交中击败了76.02% 的用户
内存消耗：15.3 MB, 在所有 Python3 提交中击败了36.67% 的用户
通过测试用例：8 / 8

```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        res = []
        def dfs(left, right, now):
            # 找当前括号数的所有结果
            if right < left:
                return
            if left == 0 and right == 0:
                res.append(now)
                return

            if left >= 1:
                dfs(left-1, right, now+"(")
            if right >= 1:
                dfs(left, right-1, now+")")
        dfs(n, n, "")
        return res
```
**Tag: 字符串、动态规划、回溯**

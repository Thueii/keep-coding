# 最长有效括号

Link => [最长有效括号](https://leetcode-cn.com/problems/longest-valid-parentheses/)

题目：给你一个只包含 '(' 和 ')' 的字符串，找出最长有效（格式正确且连续）括号子串的长度。

> 示例 1：<br />
> 输入：s = "(()"<br />
> 输出：2<br />
> 
> 示例 2：<br />
> 输入：s = ")()())"<br />
> 输出：4<br />
> 
> 示例 3：<br />
> 输入：s = ""<br />
> 输出：0<br />

```python
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        length = len(s)
        if s == "" or s == "(" or s == ")":
            return 0

        res_b = [0 for i in range(length)]
        list1 = []
        for i in range(length):
            if len(list1) == 0 or s[i] == "(":
                list1.append([s[i], i])
            elif list1[-1][0] == "(":
                res_b[list1[-1][1]] = 1
                res_b[i] = 1
                list1.pop()
        flag = False
        count_list = []
        count = 0
        for x in res_b:
            if x == 1:
                if flag:
                    count += 1
                else:
                    flag = True
                    count = 1
            else:
                flag = False
                count_list.append(count)
                count = 0
        count_list.append(count)
        return max(count_list)
```
改进：
```python
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        length = len(s)
        if s == "" or s == "(" or s == ")":
            return 0
        stack = [-1]
        length = 0
        max_length = 0
        for i in range(len(s)):
            if s[i] == "(":
                stack.append(i)
            else:
                stack.pop()
                if not stack:
                    stack.append(i)
                else:
                    length = i - stack[-1]
                    max_length = max(max_length, length)
        return max_length
```
改进：
```python
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        length = len(s)

        if length == 0 or length == 1:
            return 0

        dp = [0] * length

        for index in range(length):
            if index == 0:
                dp[index] = 0
                continue
            if s[index] == "(":
                dp[index] = 0
            elif s[index - 1] == "(":
                if index - 2 >= 0:
                    dp[index] = dp[index - 2] + 2
                else:
                    dp[index] = 2
            else:
                if index - dp[index - 1] - 1 >= 0 and s[index - dp[index - 1] - 1] == "(":
                    dp[index] = dp[index - 1] + 2 + dp[index - dp[index - 1] - 2]
                else:
                    dp[index] = 0

        return max(dp)
```
执行用时：36 ms, 在所有 Python3 提交中击败了92.29% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了75.86% 的用户
通过测试用例：231 / 231

**Tag: 栈、字符串、动态规划**

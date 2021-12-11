# 删除无效的括号

Link => [删除无效的括号](https://leetcode-cn.com/problems/remove-invalid-parentheses/)

## 题目
给你一个由若干括号和字母组成的字符串 s ，删除最小数量的无效括号，使得输入的字符串有效。

返回所有可能的结果。答案可以按 任意顺序 返回。

**示例1**
>输入：s = "()())()"<br />
>输出：["(())()","()()()"]<br />

**示例2**
>输入：s = "(a)())()"<br />
>输出：["(a())()","(a)()()"]<br />

**执行结果：通过 显示详情**
深度优先搜索，先找到多出来的左右的个数，再挨个儿去掉看看行不行，确实很费时。但是没想到这么费= =，就这还是看答案才写出来的，，

- 执行用时：5192 ms, 在所有 Python3 提交中击败了5.04% 的用户
内存消耗：27.2 MB, 在所有 Python3 提交中击败了5.02% 的用户
通过测试用例：127 / 127

```python
class Solution:
    def removeInvalidParentheses(self, s: str) -> List[str]:
        lremove = 0
        rremove = 0
        for i in range(len(s)):
            if s[i] == "(":
                lremove += 1
            elif s[i] == ")":
                if lremove != 0:
                    lremove -= 1
                else:
                    rremove += 1
        def is_valid(s):
            stack = []
            for i in range(len(s)):
                if s[i] == "(":
                    stack.append(s[i])
                elif s[i] == ")":
                    if not stack or stack.pop() != "(":
                        return False
            if stack:
                return False
            else:
                return True

        res = []

        def dfs(lremove, rremove, now):
            print(lremove, rremove)
            if lremove == 0 and rremove == 0:
                if is_valid(now):
                    res.append(now)
                return
            
            for i in range(len(now)):
                if i > 0 and now[i] == now[i-1]:
                    continue
                if lremove + rremove > len(now[i::]):
                    return
                if lremove > 0 and now[i] == "(":
                    dfs(lremove-1, rremove, now[:i]+now[i+1::])
                elif rremove > 0 and now[i] == ")":
                    dfs(lremove, rremove-1, now[:i]+now[i+1::])

        dfs(lremove, rremove, s)

        return list(set(res))
```
**改进**
仔细想一想，题目要给出去除最少的括号，就是要满足广度优先搜索的性质
此题要注意及时去重，除去不必要的计算！！

- 执行用时：120 ms, 在所有 Python3 提交中击败了49.99% 的用户
内存消耗：15.5 MB, 在所有 Python3 提交中击败了11.14% 的用户
通过测试用例：127 / 127
```python
class Solution:
    def removeInvalidParentheses(self, s: str) -> List[str]:
        stack = [s]

        def isValid(s):
            count = 0
            for c in s:
                if c == '(':
                    count += 1
                elif c == ')':
                    count -= 1
                    if count < 0:
                        return False
            return count == 0

        res = []
        flag = False
        if isValid(s):
            return [s]

        while True:
            tmp = []
            while stack:
                cur = stack.pop()
                for i in range(len(cur)):
                    if cur[i] != "(" and cur[i] != ")":
                        continue
                    if i > 0 and cur[i] == cur[i-1]:
                        continue
                    tmp.append(cur[:i]+cur[i+1:])

            stack = list(set(tmp))  # 在这里去重，免去判断太多重复的    是否合理
            for i in stack:
                if isValid(i):
                    res.append(i)
            if res:
                return res
```

**Tag: 字符串、广度优先搜索、回溯**

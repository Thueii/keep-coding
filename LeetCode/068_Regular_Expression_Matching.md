# 正则表达式匹配

Link => [正则表达式匹配](https://leetcode-cn.com/problems/regular-expression-matching/)

## 题目
给你一个字符串 s 和一个字符规律 p，请你来实现一个支持 '.' 和 '*' 的正则表达式匹配。

    '.' 匹配任意单个字符
    '*' 匹配零个或多个前面的那一个元素

所谓匹配，是要涵盖 整个 字符串 s的，而不是部分字符串。

**示例1**
>输入：s = "aa" p = "a"<br />
>输出：false<br />
>解释："a" 无法匹配 "aa" 整个字符串。<br />

**示例2**
>输入：s = "aa" p = "a*"<br />
>输出：true<br />
>解释：因为 '*' 代表可以匹配零个或多个前面的那一个元素, 在这里前面的元素就是 'a'。因此，字符串 "aa" 可被视为 'a' 重复了一次。<br />

**执行结果：通过 显示详情**
参考答案 [两种思路：递归 & 动态规划，清晰易懂](https://leetcode-cn.com/problems/regular-expression-matching/solution/liang-chong-si-lu-di-gui-dong-tai-gui-hu-gh69/)

- 执行用时：1260 ms, 在所有 Python3 提交中击败了5.14% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了40.91% 的用户
通过测试用例：353 / 353

```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        # 应该倒着想
        # 递归试一下
        def dfs(i, j):
            if j == len(p):
                return i == len(s)

            if j+1 < len(p) and p[j+1] == "*" and i<len(s) and p[j] in {s[i], "."}:
                return dfs(i+1, j) or dfs(i, j+2)
            elif j+1 < len(p) and p[j+1] == "*" and (i>=len(s) or p[j] not in {s[i], "."}):
                return dfs(i, j+2)
            elif j+1 < len(p) and p[j+1] != "*" and i<len(s) and p[j] in {s[i], "."}:
                return dfs(i+1, j+1)
            elif j+1 < len(p) and p[j+1] != "*" and (i>=len(s) or p[j] not in {s[i], "."}):
                return False
            else:
                return i<len(s) and p[j] in {s[i], "."} and dfs(i+1, j+1) # 只能完全匹配了，因为是最后一个字符了
        return dfs(0, 0)
```
**改进**
因为递归过程存在重复子问题，所以可用加一个备忘录，将状态保存，提高效率。

- 执行用时：44 ms, 在所有 Python3 提交中击败了84.28% 的用户
内存消耗：15.4 MB, 在所有 Python3 提交中击败了5.06% 的用户
通过测试用例：353 / 353

```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        # 应该倒着想
        # 递归试一下
        memo = [[-1 for _ in range(len(p))] for _ in range(len(s) + 1)]  # -1 表示未记

        def dfs(i, j):
            if j == len(p):
                return i == len(s)
            if memo[i][j] != -1:  # 已记录，直接返回
                return memo[i][j]
            if j+1 < len(p) and p[j+1] == "*" and i<len(s) and p[j] in {s[i], "."}:
                memo[i][j] = dfs(i+1, j) or dfs(i, j+2)
            elif j+1 < len(p) and p[j+1] == "*" and (i>=len(s) or p[j] not in {s[i], "."}):
                memo[i][j] = dfs(i, j+2)
            elif j+1 < len(p) and p[j+1] != "*" and i<len(s) and p[j] in {s[i], "."}:
                memo[i][j] = dfs(i+1, j+1)
            elif j+1 < len(p) and p[j+1] != "*" and (i>=len(s) or p[j] not in {s[i], "."}):
                memo[i][j] = False
            else:
                memo[i][j] = i<len(s) and p[j] in {s[i], "."} and dfs(i+1, j+1)
            return memo[i][j]
        return dfs(0, 0)x(res,j-i)
        return res
```

**2022/03/16**
- 执行用时：52 ms, 在所有 Python3 提交中击败了66.35% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了38.03% 的用户
通过测试用例：353 / 353

```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        dp = [[False] * (len(s)+1) for _ in range(len(p)+1)]

        dp[0][0] = True
        s = list(s)
        p = list(p)
        s.insert(0, "")
        p.insert(0, "")

        for i in range(1, len(dp)):
            for j in range(len(dp[0])):
                if p[i] == ".":
                    if j-1>=0 and dp[i-1][j-1]:
                        dp[i][j] = True
                elif p[i] == "*":
                    if dp[i-1][j]:
                        dp[i][j] = True
                        flag = False
                    elif dp[i-2][j]:
                        dp[i][j] = True
                        flag = True
                    elif j-1>=0 and dp[i][j-1] and not flag and (s[j] == s[j-1] or p[i-1] == "."):
                        dp[i][j] = True
                    else:
                        flag = False
                elif s[j] == p[i]:
                    if j-1 >= 0 and dp[i-1][j-1]:
                        dp[i][j] = True
        return dp[-1][-1]
```
**Tag: 递归、字符串、动态规划**

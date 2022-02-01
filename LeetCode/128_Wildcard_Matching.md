# 通配符匹配

Link => [通配符匹配](https://leetcode-cn.com/problems/wildcard-matching/)

**题目**

    给定一个字符串 (s) 和一个字符模式 (p) ，实现一个支持 '?' 和 '*' 的通配符匹配。

    '?' 可以匹配任何单个字符。
    '*' 可以匹配任意字符串（包括空字符串）。

    两个字符串完全匹配才算匹配成功。

    说明:

        s 可能为空，且只包含从 a-z 的小写字母。
        p 可能为空，且只包含从 a-z 的小写字母，以及字符 ? 和 *。


**示例1**

    输入:
    s = "aa"
    p = "a"
    输出: false
    解释: "a" 无法匹配 "aa" 整个字符串。

**示例 2**

    输入:
    s = "aa"
    p = "*"
    输出: true
    解释: '*' 可以匹配任意字符串。

**示例 3**

    输入:
    s = "cb"
    p = "?a"
    输出: false
    解释: '?' 可以匹配 'c', 但第二个 'a' 无法匹配 'b'。

**示例 4**

    输入:
    s = "adceb"
    p = "*a*b"
    输出: true
    解释: 第一个 '*' 可以匹配空字符串, 第二个 '*' 可以匹配字符串 "dce".

**结果**
棋盘原理

- 执行用时：920 ms, 在所有 Python3 提交中击败了9.30% 的用户
内存消耗：23.2 MB, 在所有 Python3 提交中击败了29.67% 的用户
通过测试用例：1811 / 1811

```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        
        dp = [[False]*(len(s)+1) for i in range(len(p)+1)]
        dp[0][0] = True
        for i in range(len(dp)):
            flag = False
            for j in range(len(dp[i])):
                if dp[i][j] == True:
                    continue
                elif flag:
                    dp[i][j] = True
                elif (i-1>=0 and j-1 >=0) and dp[i-1][j-1] and s[j-1] == p[i-1]:
                    dp[i][j] = True
                elif (i-1>=0) and dp[i-1][j] and p[i-1] == "*":
                    flag = True
                    dp[i][j] = True
                elif (i-1>=0 and j-1 >=0) and dp[i-1][j-1] and p[i-1] == "?":
                    dp[i][j] = True
        return dp[-1][-1]
```
**Tag: 字符串、回溯**

# 最长回文子串

Link => [最长回文子串
](https://leetcode-cn.com/problems/longest-palindromic-substring/)

**题目：给你一个字符串 s，找到 s 中最长的回文子串。**
>示例1：<br />
>输入：s = "babad"<br />
>输出："bab"<br />
>解释："aba" 同样是符合题意的答案。<br />
> 
> 示例 2：<br />
>输入：s = "cbbd"<br />
>输出："bb"<br />
> 
> 示例 3：<br />
>输入：s = "a"<br />
>输出："a"<br />

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)
        if n == 1:
            return s
        if n == 2:
            if s[0] == s[1]:
                return s
            else:
                return s[0]
        dp = [[False] * n for i in range(n)]
        long = 0
        resl = None
        resr = None
        for right in range(1,n):
            for left in range(0, right):
                if (s[left] == s[right]) and (right-left<3 or dp[left+1][right-1]):
                    if right-left+1>long:
                        resl = left
                        resr = right
                        long = right-left+1
                    dp[left][right] = True
        if resl is None:
            return s[0]
        return s[resl:resr+1]
```
**2022/03/15**
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        # 中心扩展，注意双中心的情况 时间复杂度O(n^2) 空间复杂度 O(1)

        length = len(s)
        start = 0
        max_len = 1
        for i in range(length):
            size = 1
            while i-size >= 0 and i+size<length and s[i-size] == s[i+size]:
                if 2*size+1>max_len:
                    max_len = 2*size+1
                    start = i-size
                size += 1
            if i + 1 == length:
                break
            size = 0
            while i-size >= 0 and i+size+1 < length and s[i-size] == s[i+size+1]:
                if 2*size+2>max_len:
                    max_len = 2*size+2
                    start = i-size
                size += 1
        return s[start:start+max_len]

class Solution:
    def longestPalindrome(self, s: str) -> str:
        # 动态规划，慢一些 时间复杂度 O(n^2) 空间复杂度 O(n^2)

        dp = [[True] * len(s) for i in range(len(s))]
        max_len = 1
        res = s[0]
        for length in range(len(s) - 1):
            for i in range(len(s)):
                j = i + length + 1
                if j >= len(s):
                    break
                if s[i] != s[j] or not dp[i + 1][j - 1]:
                    dp[i][j] = False
                else:
                    if j - i + 1 > max_len:
                        max_len = j - i + 1
                        res = s[i:j+1]
        return res
```
**Tag: 字符串、动态规划**

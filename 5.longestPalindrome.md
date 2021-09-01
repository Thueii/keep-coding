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

**Tag: 字符串、动态规划**

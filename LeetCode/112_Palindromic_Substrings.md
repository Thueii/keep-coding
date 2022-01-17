# 回文子串

Link => [回文子串](https://leetcode-cn.com/problems/palindromic-substrings/)

## 题目

    给你一个字符串 s ，请你统计并返回这个字符串中 回文子串 的数目。

    回文字符串 是正着读和倒过来读一样的字符串。

    子字符串 是字符串中的由连续字符组成的一个序列。

    具有不同开始位置或结束位置的子串，即使是由相同的字符组成，也会被视作不同的子串。

**示例1**

    输入：s = "abc"
    输出：3
    解释：三个回文子串: "a", "b", "c"

**示例2**

    输入：s = "aaa"
    输出：6
    解释：6个回文子串: "a", "a", "a", "aa", "aa", "aaa"

**执行结果：通过 显示详情**
区间dp

- 执行用时：220 ms, 在所有 Python3 提交中击败了32.52% 的用户
内存消耗：22.7 MB, 在所有 Python3 提交中击败了16.96% 的用户
通过测试用例：130 / 130

```python
class Solution:
    def countSubstrings(self, s: str) -> int:
        res = 0
        n = len(s)
        dp = [[False] * n for i in range(n)]
        for i in range(n-1, -1, -1):
            for j in range(i, n):
                if j-i==0:
                    dp[i][j]= True
                    res += 1
                elif j-i==1:
                    if s[i]==s[j]:
                        dp[i][j]= True
                        res += 1
                else:
                    if s[i]==s[j] and dp[i+1][j-1] == True:
                        dp[i][j]= True
                        res += 1
        return res
```

**Tag: 字符串、动态规划**

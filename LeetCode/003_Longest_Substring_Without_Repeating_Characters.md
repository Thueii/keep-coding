# 无重复字符的最长子串

Link => [无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

题目：给定一个字符串 s ，请你找出其中不含有重复字符的 最长子串 的长度。

> 示例 1：<br />
> 输入: s = "abcabcbb"<br />
> 输出: 3<br />
> 解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。<br />
> 
> 示例 2：<br />
> 输入: s = "bbbbb"<br />
> 输出: 1<br />
> 解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。<br />
>
> 示例 3：<br />
> 输入: s = "pwwkew"<br />
> 输出: 3<br />
> 解释: 因为无重复字符的最长子串是  "wke"，所以其长度为 3。请注意，你的答案必须是 子串 的长度，"pwke"  是一个子序列，不是子串。<br />
>
> 示例 4:<br />
> 输入: s = ""<br />
> 输出: 0<br />

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if s == "":
            return 0
        left = 0
        adict = {}
        res = []
        for i, v in enumerate(s):
            if not adict.get(v):
                res.append(i-left+1)
            else:
                if adict[v] >= left:
                    left = adict[v] + 1
                else:
                    res.append(i-left+1)

            adict[v] = i
        return max(res)
```
**2022.3.14**
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        adict = {}
        start = 0
        res = 0
        for idx in range(len(s)):
            if s[idx] not in adict or adict[s[idx]] < start:
                res = max(res, idx - start + 1)
            else:
                start = adict[s[idx]] + 1
            adict[s[idx]] = idx
        return res
```
**Tag: 哈希表、字符串、滑动窗口**

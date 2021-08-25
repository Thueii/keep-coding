# 无重复字符的最长子串
[[无重复字符的最长子串] https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/ ]
::Tag: 哈希表、字符串、滑动窗口::
> 给定一个字符串 s ，请你找出其中不含有重复字符的 最长子串 的长度。
> 示例 1：
> 输入: s = "abcabcbb"
> 输出: 3 
> 解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
> 
> 示例 2：
> 输入: s = "bbbbb"
> 输出: 1
> 解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
> 
> 示例 3：
> 输入: s = "pwwkew"
> 输出: 3
> 解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
> 
> 示例 4:
> 输入: s = ""
> 输出: 0

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

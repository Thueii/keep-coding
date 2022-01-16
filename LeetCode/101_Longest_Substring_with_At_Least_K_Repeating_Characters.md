# 至少有 K 个重复字符的最长子串

Link => [至少有 K 个重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-with-at-least-k-repeating-characters/)

## 题目

    给你一个字符串 s 和一个整数 k ，请你找出 s 中的最长子串， 要求该子串中的每一字符出现次数都不少于 k 。返回这一子串的长度。  

**示例1**

    输入：s = "aaabb", k = 3
    输出：3
    解释：最长子串为 "aaa" ，其中 'a' 重复了 3 次。

**示例2**

    输入：s = "ababbc", k = 2
    输出：5
    解释：最长子串为 "ababb" ，其中 'a' 重复了 2 次， 'b' 重复了 3 次。

**执行结果：通过 显示详情**
只能说，对于这种最长的子串，注意可以用递归的方式，在内部切割

- 执行用时：32 ms, 在所有 Python3 提交中击败了80.39% 的用户
内存消耗：14.9 MB, 在所有 Python3 提交中击败了93.64% 的用户
通过测试用例：35 / 35

```python
class Solution:
    def longestSubstring(self, s: str, k: int) -> int:
        if len(s) < k:
            return 0
        for c in set(s):
            if s.count(c) < k:
                return max(self.longestSubstring(i, k) for i in s.split(c))
        return len(s)
```
**Tag: 哈希表、字符串、滑动窗口、分治**

# 复原 IP 地址

Link => [复原 IP 地址](https://leetcode-cn.com/problems/restore-ip-addresses/)

**题目**

    有效 IP 地址 正好由四个整数（每个整数位于 0 到 255 之间组成，且不能含有前导 0），整数之间用 '.' 分隔。

        例如："0.1.2.201" 和 "192.168.1.1" 是 有效 IP 地址，但是 "0.011.255.245"、"192.168.1.312" 和 "192.168@1.1" 是 无效 IP 地址。

    给定一个只包含数字的字符串 s ，用以表示一个 IP 地址，返回所有可能的有效 IP 地址，这些地址可以通过在 s 中插入 '.' 来形成。你不能重新排序或删除 s 中的任何数字。你可以按 任何 顺序返回答案。

**示例1**

    输入：s = "25525511135"
    输出：["255.255.11.135","255.255.111.35"]

**示例 2**

    输入：s = "0000"
    输出：["0.0.0.0"]

**示例 3**

    输入：s = "1111"
    输出：["1.1.1.1"]

**示例 4**

    输入：s = "010010"
    输出：["0.10.0.10","0.100.1.0"]

**结果**
用记录当前串+"此次的"+"." 和剩下的字符串
- 执行用时：36 ms, 在所有 Python3 提交中击败了69.44% 的用户
内存消耗：15 MB, 在所有 Python3 提交中击败了66.06% 的用户
通过测试用例：145 / 145
```python
class Solution:
    def restoreIpAddresses(self, s: str) -> List[str]:
        res = []
        def dfs(left_count, now, s):
            if left_count < 0:
                if len(s) == 0:
                    res.append(now[:-1])
                return

            for i in range(len(s)):
                if s[:i+1] == "0" or (not s[:i+1].startswith("0") and 0<=int(s[:i+1])<=255):
                    dfs(left_count-1, now+s[:i+1]+".", s[i+1:])
            return

        dfs(3, "", s)

        return res
```
**Tag: 字符串、回溯**

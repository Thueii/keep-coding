# 最长公共前缀

Link => [最长公共前缀](https://leetcode-cn.com/problems/longest-common-prefix/)

## 题目

    编写一个函数来查找字符串数组中的最长公共前缀。

    如果不存在公共前缀，返回空字符串 ""。

**示例1**

    输入：strs = ["flower","flow","flight"]
    输出："fl"

**示例2**

    输入：strs = ["dog","racecar","car"]
    输出：""
    解释：输入不存在公共前缀。

**执行结果：通过 显示详情**
用字典序最长的和字典序最短的比较就行了

- 执行用时：36 ms, 在所有 Python3 提交中击败了54.08% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了32.27% 的用户
通过测试用例：123 / 123

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        if not strs:
            return ""
        min_str = min(strs)
        max_str = max(strs)
        res = ""
        for i in range(len(min_str)):
            if min_str[i] != max_str[i]:
                break
            else:
                res = min_str[:i+1]
        return res
```
**Tag: 字符串**

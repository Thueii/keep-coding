# 回文数

Link => [回文数](https://leetcode-cn.com/problems/palindrome-number/)

## 题目
    给你一个整数 x ，如果 x 是一个回文整数，返回 true ；否则，返回 false 。

    回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

    例如，121 是回文，而 123 不是。


**示例1**

    输入：x = 121
    输出：true

**示例2**

    输入：x = -121
    输出：false
    解释：从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。

**执行结果：通过 显示详情**

- 执行用时：64 ms, 在所有 Python3 提交中击败了56.37% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了11.76% 的用户
通过测试用例：11510 / 11510

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if x < 0: return False
        if 0 <= x < 10: return True
        if not x % 10: return False
        if x < 100: return x // 10 == x % 10

        # x = 12321  12 123
        reverse = 0
        while x > reverse:
            quo = x % 10
            reverse = reverse * 10 + quo
            x //= 10
        return x == reverse or x == reverse//10
```
**Tag: 数学**

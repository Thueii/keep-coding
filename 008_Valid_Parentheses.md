# 有效的括号

Link => [有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)

题目：给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串 s ，判断字符串是否有效。

有效字符串需满足：
    1. 左括号必须用相同类型的右括号闭合。
    2. 左括号必须以正确的顺序闭合。

>示例1：<br />
>输入：s = "()"<br />
>输出：true<br />
> 
> 示例 2：<br />
>输入："()[]{}"<br />
>输出：true<br />

> 示例 3：<br />
>输入：x = "(]"<br />
>输出：false<br />

```python
class Solution:
    def isValid(self, s: str) -> bool:
        mapping = {
            ")": "(",
            "}": "{",
            "]": "["
        }
        stack = []
        for each_str in s:
            if len(stack) == 0 or stack[-1] != mapping.get(each_str):
                stack.append(each_str)
            else:
                stack.pop()
        if len(stack) != 0:
            return False
        else:
            return True
```

**Tag: 栈、字符串**

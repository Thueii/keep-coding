# 字符串解码

Link => [字符串解码](https://leetcode-cn.com/problems/decode-string/)

给定一个经过编码的字符串，返回它解码后的字符串。

编码规则为: k[encoded_string]，表示其中方括号内部的 encoded_string 正好重复 k 次。注意 k 保证为正整数。

你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。

此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 k ，例如不会出现像 3a 或 2[4] 的输入。

>输入：s = "3[a]2[bc]"<br />
>输出："aaabcbc"<br />

>输入：s = "3[a2[c]]"<br />
>输出："accaccacc"<br />

执行结果：
通过
显示详情

添加备注
执行用时：28 ms, 在所有 Python3 提交中击败了84.91% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了5.44% 的用户
通过测试用例：34 / 34

```python
class Solution:
    def decodeString(self, s: str) -> str:
        stack = []
        for i in s:
            if i == "]":
                s = ""
                while True:
                    now = stack.pop()
                    if now.isalpha() or len(now)>1:
                        s = now + s
                    else:
                        if now.isdigit():
                            num = ""
                            num = num + now
                            while stack and stack[-1].isdigit():
                                now = stack.pop()
                                num = now + num

                            num = int(num)

                            s = num * s
                            stack.append(s)
                            break                   
            else:
                stack.append(i)
        return "".join(stack)
```
**Tag: 栈、递归、字符串**

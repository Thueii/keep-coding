# 整数反转

Link => [整数反转
](https://leetcode-cn.com/problems/reverse-integer/)

**题目：给你一个 32 位的有符号整数 x ，返回将 x 中的数字部分反转后的结果。如果反转后整数超过 32 位的有符号整数的范围 [−231,  231 − 1] ，就返回 0。假设环境不允许存储 64 位整数（有符号或无符号）。
**

>示例1：<br />
>输入：x = 123<br />
>输出：321<br />
> 
> 示例 2：<br />
>输入：x = -123<br />
>输出：-321<br />

> 示例 3：<br />
>输入：x = 120<br />
>输出：21<br />

```python
class Solution:
    def reverse(self, x: int) -> int:
        str_x = str(x)
        if str_x[0] == "-":
            str_x = str_x[1:]
            x = int("-"+str_x[::-1])
        else:
            x = int(str_x[::-1])
        if x < -2**31 or x > 2**31 -1:
            return 0
        else:
            return x
```

**Tag: 数学**

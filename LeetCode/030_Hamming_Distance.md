# 汉明距离

Link => [汉明距离](https://leetcode-cn.com/problems/hamming-distance/)

## 题目
两个整数之间的 汉明距离 指的是这两个数字对应二进制位不同的位置的数目。

给你两个整数 x 和 y，计算并返回它们之间的汉明距离。

**示例1**
>输入：x = 1, y = 4<br />
>输出：2<br />
>解释：
>1   (0 0 0 1)<br />
>4   (0 1 0 0)<br />
>       ↑   ↑<br />
>上面的箭头指出了对应二进制位不同的位置。<br />

**示例2**
>输入：x = 3, y = 1<br />
>输出：1<br />

**执行结果：通过 显示详情**

- 执行用时：24 ms, 在所有 Python3 提交中击败了96.81% 的用户
内存消耗：14.9 MB, 在所有 Python3 提交中击败了53.99% 的用户
通过测试用例：149 / 149

```python
class Solution:
    def hammingDistance(self, x: int, y: int) -> int:
        x = bin(x)
        y = bin(y)
        res = 0
        lo = len(x) - len(y)

        if lo > 0:
            y = "0b" + "0" * lo + y[2::]
        elif lo < 0:
            x = "0b" + "0" * (-lo) + x[2::]

        for i in range(len(x)):
            res += (x[i] != y[i])
        return res
```
**改进：**

- 两个数字的异或结果就是题意的一个位对一个位的异或再转换成是禁止的结果!!!!!

- 执行结果：
通过
显示详情

- 添加备注
执行用时：28 ms, 在所有 Python3 提交中击败了86.76% 的用户
内存消耗：15 MB, 在所有 Python3 提交中击败了31.51% 的用户
通过测试用例：149 / 149

```python
class Solution:
    def hammingDistance(self, x: int, y: int) -> int:
        # 两个数字的异或结果就是题意的一个位对一个位的异或再转换成是禁止的结果!!!!!
        return bin(x ^ y).count('1')
```
**Tag: 位运算**

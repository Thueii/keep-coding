# 比特位计数

Link => [比特位计数](https://leetcode-cn.com/problems/counting-bits/)

## 题目
给你一个整数 n ，对于 0 <= i <= n 中的每个 i ，计算其二进制表示中 1 的个数 ，返回一个长度为 n + 1 的数组 ans 作为答案。

**示例1**
>输入：n = 2<br />
>输出：[0,1,1]<br />
>解释：<br />
>0 --> 0<br />
>1 --> 1<br />
>2 --> 10<br />

**示例2**
>输入：n = 5
>输出：[0,1,1,2,1,2]
>解释：
>0 --> 0<br />
>1 --> 1<br />
>2 --> 10<br />
>3 --> 11<br />
>4 --> 100<br />
>5 --> 101<br />

执行结果：
通过
显示详情

添加备注
执行用时：132 ms, 在所有 Python3 提交中击败了10.01% 的用户
内存消耗：15.5 MB, 在所有 Python3 提交中击败了96.93% 的用户
通过测试用例：15 / 15

```python
class Solution:
    def countBits(self, n: int) -> List[int]:
        res = []
        for each in range(n+1):
            count = 0
            while each // 2 != 0:
                if each % 2 == 1:
                    count += 1
                each = each // 2
            if each != 0:
                count += 1
            res.append(count)
        return res
```
改进：
直接用bin().count("1")
执行结果：
通过
显示详情

添加备注
执行用时：36 ms, 在所有 Python3 提交中击败了93.06% 的用户
内存消耗：15.6 MB, 在所有 Python3 提交中击败了89.75% 的用户
通过测试用例：15 / 15
```python
class Solution:
    def countBits(self, num: int) -> List[int]:
        # 时间复杂度：O(N∗sizeof(int))
        # 空间复杂度：O(1)返回数组不计入空间复杂度中。

        res = []
        for i in range(num + 1):
            res.append(bin(i).count("1"))
        return res
```
改进：
动态规划，前身用递归理解一下
```python
class Solution(object):
    # 递归
    def countBits(self, num):
        res = []
        for i in range(num + 1):
            res.append(self.count(i))
        return res
    
    def count(self, num):
        if num == 0:
            return 0
        if num % 2 == 1:
            return self.count(num - 1) + 1
        return self.count(num // 2)

```
动态规划，就是递归反过来想，位运算太妙了
执行结果：
通过
显示详情

添加备注
执行用时：32 ms, 在所有 Python3 提交中击败了97.91% 的用户
内存消耗：15.7 MB, 在所有 Python3 提交中击败了60.53% 的用户
通过测试用例：15 / 15
```python
class Solution:
    def countBits(self, num: int) -> List[int]:
        res = [0 for each in range(num + 1)]
        for each in range(num + 1):
            if each == 0:
                continue
            res[each] = res[each >> 1] + (each & 1)
        return res
```
**Tag: 位运算、动态规划**

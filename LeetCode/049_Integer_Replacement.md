# 整数替换

Link => [整数替换](https://leetcode-cn.com/problems/integer-replacement/)

## 题目
给定一个正整数 n ，你可以做如下操作：

    如果 n 是偶数，则用 n / 2替换 n 。
    如果 n 是奇数，则可以用 n + 1或n - 1替换 n 。

n 变为 1 所需的最小替换次数是多少？


**示例1**
>输入：n = 8<br />
>输出：3<br />
>说明：8 -> 4 -> 2 -> 1<br />

**示例2**
>输入：n = 7<br />
>输出：4<br />
>说明：7 -> 8 -> 4 -> 2 -> 1
>或 7 -> 6 -> 3 -> 2 -> 1<br />

**执行结果：通过 显示详情**
没啥，主要是要记录做过的，记得+1

- 执行用时：28 ms, 在所有 Python3 提交中击败了93.41% 的用户
内存消耗：14.8 MB, 在所有 Python3 提交中击败了88.37% 的用户
通过测试用例：47 / 47

```python
class Solution:
    def integerReplacement(self, n: int) -> int:
        times = 0
        m = {}
        def find(n, times):
            if n == 1:
                return times
            if n in m:
                return m[n] + times
            if n % 2:
                times += 1
                min_times = min(find(n+1, times), find(n-1, times))
                m[n] = min_times - times + 1
                return min_times
            else:
                times += 1
                min_times = find(n/2, times)
                m[n] = min_times - times + 1
                return min_times

        return find(n, times)
```

**Tag: 贪心、位运算、记忆化搜索、动态规划**

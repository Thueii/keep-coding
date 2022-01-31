# 外观数列

Link => [外观数列](https://leetcode-cn.com/problems/count-and-say/)

## 题目

    给定一个正整数 n ，输出外观数列的第 n 项。

    「外观数列」是一个整数序列，从数字 1 开始，序列中的每一项都是对前一项的描述。

    你可以将其视作是由递归公式定义的数字字符串序列：

        countAndSay(1) = "1"
        countAndSay(n) 是对 countAndSay(n-1) 的描述，然后转换成另一个数字字符串。

    前五项如下：

    1.     1
    2.     11
    3.     21
    4.     1211
    5.     111221
    第一项是数字 1 
    描述前一项，这个数是 1 即 " 一 个 1 "，记作 "11"
    描述前一项，这个数是 11 即 " 二 个 1 " ，记作 "21"
    描述前一项，这个数是 21 即 " 一 个 2 + 一 个 1 " ，记作 "1211"
    描述前一项，这个数是 1211 即 " 一 个 1 + 一 个 2 + 二 个 1 " ，记作 "111221"
    要 描述 一个数字字符串，首先要将字符串分割为 最小 数量的组，每个组都由连续的最多 相同字符 组成。然后对于每个组，先描述字符的数量，然后描述字符，形成一个描述组。要将描述转换为数字字符串，先将每组中的字符数量用数字替换，再将所有描述组连接起来。

**示例1**

    输入：n = 1
    输出："1"
    解释：这是一个基本样例。

**示例2**

    输入：n = 4
    输出："1211"
    解释：
    countAndSay(1) = "1"
    countAndSay(2) = 读 "1" = 一 个 1 = "11"
    countAndSay(3) = 读 "11" = 二 个 1 = "21"
    countAndSay(4) = 读 "21" = 一 个 2 + 一 个 1 = "12" + "11" = "1211"

**执行结果：通过 显示详情**
注意不要用count来技术可以多用双指针，记录索引，也等于记录了那个树字

- 执行用时：40 ms, 在所有 Python3 提交中击败了90.34% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了23.44% 的用户
通过测试用例：30 / 30

```python
class Solution:
    def countAndSay(self, n: int) -> str:
        # 迭代
        now = "1"
        for i in range(2, n+1):
            last_idx = 0
            tmp = ""
            for j in range(len(now)):
                if now[j] != now[last_idx]:
                    tmp += (str(j-last_idx)+now[last_idx])
                    last_idx = j
            tmp += (str(len(now)-last_idx)+now[last_idx])
            now = tmp
        return now
```
**递归来一个**
感觉比较好想，其实这题和迭代差不多哦，主要用双指针来记录就好了

- 执行用时：44 ms, 在所有 Python3 提交中击败了78.65% 的用户
内存消耗：15 MB, 在所有 Python3 提交中击败了58.85% 的用户
通过测试用例：30 / 30

```python
class Solution:
    def countAndSay(self, n: int) -> str:
        
        def dfs(n):
            if n == 1:
                return "1"
            else:
                last_index = 0
                word = dfs(n-1)
                res = ""
                for i in range(len(word)):
                    if word[i] != word[last_index]:
                        res += str(i-last_index) + word[last_index]
                        last_index = i
                res += str(len(word)-last_index) + word[last_index]
                return res
        return dfs(n)
```
**Tag: 字符串**

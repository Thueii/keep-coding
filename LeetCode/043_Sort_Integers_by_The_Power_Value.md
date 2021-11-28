# 将整数按权重排序

Link => [将整数按权重排序](https://leetcode-cn.com/problems/sort-integers-by-the-power-value/)

## 题目
我们将整数 x 的 权重 定义为按照下述规则将 x 变成 1 所需要的步数：

    如果 x 是偶数，那么 x = x / 2
    如果 x 是奇数，那么 x = 3 * x + 1

比方说，x=3 的权重为 7 。因为 3 需要 7 步变成 1 （3 --> 10 --> 5 --> 16 --> 8 --> 4 --> 2 --> 1）。

给你三个整数 lo， hi 和 k 。你的任务是将区间 [lo, hi] 之间的整数按照它们的权重 升序排序 ，如果大于等于 2 个整数有 相同 的权重，那么按照数字自身的数值 升序排序 。

请你返回区间 [lo, hi] 之间的整数按权重排序后的第 k 个数。

注意，题目保证对于任意整数 x （lo <= x <= hi） ，它变成 1 所需要的步数是一个 32 位有符号整数。

**示例1**
>输入：lo = 12, hi = 15, k = 2 <br />
>输出：13<br />
>解释：12 的权重为 9（12 --> 6 --> 3 --> 10 --> 5 --> 16 --> 8 --> 4 --> 2 --> 1）<br />
13 的权重为 9<br />
14 的权重为 17<br />
15 的权重为 17<br />
区间内的数按权重排序以后的结果为 [12,13,14,15] 。对于 k = 2 ，答案是第二个整数也就是 13 。<br />
注意，12 和 13 有相同的权重，所以我们按照它们本身升序排序。14 和 15 同理。<br />


**示例2**
>输入：lo = 1, hi = 1, k = 1<br />
>输出：1<br />

**执行结果：通过 显示详情**

写的非常差啊，要是改成dict存储应该会好一点

- 执行用时：5208 ms, 在所有 Python3 提交中击败了5.34% 的用户
内存消耗：15.4 MB, 在所有 Python3 提交中击败了48.09% 的用户
通过测试用例：333 / 333

```python
class Solution:
    def getKth(self, lo: int, hi: int, k: int) -> int:
        numlist = []
        footlist = []
        res_list = []
        for num in range(lo, hi+1):
            if num in numlist:
                res_list.append([num, footlist[numlist.index(num)]])
            else:
                tmp_num = num
                tmp_list = []
                while tmp_num not in numlist:
                    tmp_list.append(tmp_num)
                    if tmp_num == 1:
                        break

                    if tmp_num % 2:
                        tmp_num = tmp_num * 3 + 1
                    else:
                        tmp_num = tmp_num / 2

                for i in range(len(tmp_list)):
                    if tmp_num != 1:
                        footlist.append(footlist[numlist.index(tmp_num)] + i + 1)
                    else:
                        footlist.append(i)
                    numlist.append(tmp_list.pop())

                res_list.append([num, footlist[-1]])
        res_list.sort(key=lambda x:x[1])
        return res_list[k-1][0]
```
**改进：**
改成dict存储

- 执行用时：220 ms, 在所有 Python3 提交中击败了58.01% 的用户
内存消耗：15.3 MB, 在所有 Python3 提交中击败了56.49% 的用户
通过测试用例：333 / 333
```python
class Solution:
    def getKth(self, lo: int, hi: int, k: int) -> int:
        mem_dict = {}
        numlist = []
        footlist = []
        res_list = []
        for num in range(lo, hi+1):
            if num in mem_dict.keys():
                res_list.append([num, mem_dict[num]])
            else:
                tmp_num = num
                tmp_list = []
                while tmp_num not in mem_dict.keys():
                    tmp_list.append(tmp_num)
                    if tmp_num == 1:
                        break

                    if tmp_num % 2:
                        tmp_num = tmp_num * 3 + 1
                    else:
                        tmp_num = tmp_num / 2

                for i in range(len(tmp_list)):
                    if tmp_num != 1:
                        mem_dict[tmp_list.pop()] = mem_dict[tmp_num] + i + 1
                    else:
                        mem_dict[tmp_list.pop()] = i

                res_list.append([num, mem_dict[num]])
        res_list.sort(key=lambda x:x[1])
        return res_list[k-1][0]
```
**其他：**
第一次知道启动缓存，但是递归就是很慢，还是没我写的快哈哈哈

- 执行用时：572 ms, 在所有 Python3 提交中击败了35.11% 的用户
内存消耗：16.4 MB, 在所有 Python3 提交中击败了41.22% 的用户
通过测试用例：333 / 333
```python
from functools import lru_cache
class Solution:
    def getKth(self, lo: int, hi: int, k: int) -> int:
        @lru_cache
        def getF(x):
            if x == 1:
                return 0
            t,yu=divmod(x,2)
            return 1+ (getF(x * 3 + 1) if yu else getF(t)) 
        
        v = list(range(lo, hi + 1))
        v.sort(key=lambda x: (getF(x), x))
        return v[k - 1]
```
**Tag: 记忆化搜索、动态规划、排序**

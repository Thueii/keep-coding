# 合并区间

Link => [合并区间](https://leetcode-cn.com/problems/merge-intervals/)

## 题目

    以数组 intervals 表示若干个区间的集合，其中单个区间为 intervals[i] = [starti, endi] 。请你合并所有重叠的区间，并返回一个不重叠的区间数组，该数组需恰好覆盖输入中的所有区间。



**示例1**

    输入：intervals = [[1,3],[2,6],[8,10],[15,18]]
    输出：[[1,6],[8,10],[15,18]]
    解释：区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].


**示例2**

    输入：intervals = [[1,4],[4,5]]
    输出：[[1,5]]
    解释：区间 [1,4] 和 [4,5] 可被视为重叠区间。

**执行结果：通过 显示详情**
这么慢的吗

- 执行用时：52 ms, 在所有 Python3 提交中击败了17.59% 的用户
内存消耗：18.4 MB, 在所有 Python3 提交中击败了5.03% 的用户
通过测试用例：169 / 169

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort(key=lambda x:[x[0], x[1]])

        left = intervals[0][0]
        right = intervals[0][1]

        res = []

        for each in intervals[1::]:
            if each[0] <= right:
                if each[1] > right:
                    right = each[1]
            else:
                res.append([left, right])
                left = each[0]
                right = each[1]
        res.append([left, right])
        return res
```
**改进**
第二个排序其实不需要提高了很多

- 执行用时：40 ms, 在所有 Python3 提交中击败了64.55% 的用户
内存消耗：18.4 MB, 在所有 Python3 提交中击败了5.03% 的用户
通过测试用例：169 / 169

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort(key=lambda x:x[0])

        left = intervals[0][0]
        right = intervals[0][1]

        res = []

        for each in intervals[1::]:
            if each[0] <= right:
                right = max(right, each[1])
            else:
                res.append([left, right])
                left, right = each[0], each[1]
        res.append([left, right])
        return res
```
好像这题python只能写成这样
**Tag: 数组、排序**

# 只出现一次的数字

Link => [只出现一次的数字](https://leetcode-cn.com/problems/daily-temperatures/)

给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

说明：

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？


>输入：[2,2,1]<br />
>输出：1<br />

>输入：[4,1,2,1,2]<br />
>输出：4<br />

执行结果：
通过
显示详情

添加备注
执行用时：44 ms, 在所有 Python3 提交中击败了49.68% 的用户
内存消耗：16.5 MB, 在所有 Python3 提交中击败了86.17% 的用户
通过测试用例：61 / 61

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        nums.sort()
        from itertools import groupby 
        for k, g in groupby(nums):
            if len(list(g)) == 1:
                return k 
```
改进：
执行结果：
通过
显示详情

添加备注
执行用时：44 ms, 在所有 Python3 提交中击败了49.68% 的用户
内存消耗：16.5 MB, 在所有 Python3 提交中击败了91.10% 的用户
通过测试用例：61 / 61
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        nums.sort()
        flag = False
        while nums:
            now = nums.pop()
            if nums and nums[-1] == now:
                flag = True
            elif nums and flag == True:
                flag = False
            else:
                return now

```
改进：
执行结果：
通过
显示详情

添加备注
执行用时：36 ms, 在所有 Python3 提交中击败了87.81% 的用户
内存消耗：16.5 MB, 在所有 Python3 提交中击败了70.00% 的用户
通过测试用例：61 / 61
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        res = 0
        for i in nums:
            res ^= i
        return res
```
改进：
数学算法

执行结果：
通过
显示详情

添加备注
执行用时：24 ms, 在所有 Python3 提交中击败了99.87% 的用户
内存消耗：16.8 MB, 在所有 Python3 提交中击败了5.79% 的用户
通过测试用例：61 / 61

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:

        return sum(set(nums))*2-sum(nums)
```
**Tag: 位运算、数组**

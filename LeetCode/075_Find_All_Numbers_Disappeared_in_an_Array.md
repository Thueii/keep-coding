# 找到所有数组中消失的数字

Link => [找到所有数组中消失的数字](https://leetcode-cn.com/problems/find-all-numbers-disappeared-in-an-array/)

## 题目
给你一个含 n 个整数的数组 nums ，其中 nums[i] 在区间 [1, n] 内。请你找出所有在 [1, n] 范围内但没有出现在 nums 中的数字，并以数组的形式返回结果。

提示：<br />

    n == nums.length
    1 <= n <= 105
    1 <= nums[i] <= n

**进阶**
进阶：你能在不使用额外空间且时间复杂度为 O(n) 的情况下解决这个问题吗? 你可以假定返回的数组不算在额外空间内。<br />

**示例1**<br />

    输入：nums = [4,3,2,7,8,2,3,1]
    输出：[5,6]

**执行结果：通过 显示详情**
用了额外的空间

- 执行用时：84 ms, 在所有 Python3 提交中击败了49.03% 的用户
内存消耗：22.3 MB, 在所有 Python3 提交中击败了36.85% 的用户
通过测试用例：33 / 33

```python
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        adict = {}
        res = []
        for i in nums:
            if not adict.get(i):
                adict[i] = True
        for i in range(1, len(nums)+1):
            if not adict.get(i):
                res.append(i)
        return res
```

**改进**
这样算不算不利用额外空间

- 执行用时：60 ms, 在所有 Python3 提交中击败了89.97% 的用户
内存消耗：22.7 MB, 在所有 Python3 提交中击败了30.74% 的用户
通过测试用例：33 / 33

```python
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        res = []
        lenght = len(nums)
        nums = set(nums)
        for i in range(1, lenght+1):
            if i not in nums:
                res.append(i)
        return res
```
**改进**
好方法

- 执行用时：264 ms, 在所有 Python3 提交中击败了99.54% 的用户
内存消耗：27.1 MB, 在所有 Python3 提交中击败了50.92% 的用户
通过测试用例：61 / 61

```python
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        return list(set(range(1, len(nums) + 1)) ^ set(nums))
```
**改进**

- 执行用时：60 ms, 在所有 Python3 提交中击败了89.97% 的用户
内存消耗：24.9 MB, 在所有 Python3 提交中击败了11.52% 的用户
通过测试用例：33 / 33

```python
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        return list(set(range(1, len(nums) + 1)).difference(set(nums)))
```

**改进**
真的原地改变的办法

- 执行用时：92 ms, 在所有 Python3 提交中击败了33.86% 的用户
内存消耗：20.7 MB, 在所有 Python3 提交中击败了71.12% 的用户
通过测试用例：33 / 33

```python
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        res = []
        for i in nums:
            if nums[abs(i)-1] > 0:
                nums[abs(i)-1] *= -1
        for i in range(len(nums)):
            if nums[i] > 0:
                res.append(i+1)
        return res
```
**Tag: 数组、哈希表、滑动窗口**

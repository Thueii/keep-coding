# 在排序数组中查找元素的第一个和最后一个位置

Link => [在排序数组中查找元素的第一个和最后一个位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

## 题目
给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。

如果数组中不存在目标值 target，返回 [-1, -1]。

**进阶**

    你可以设计并实现时间复杂度为 O(log n) 的算法解决此问题吗？


**示例1**

    输入：nums = [5,7,7,8,8,10], target = 8
    输出：[3,4]

**示例2**

    输入：nums = [5,7,7,8,8,10], target = 6
    输出：[-1,-1]

**执行结果：通过 显示详情**
傻逼写法，先过再说

- 执行用时：32 ms, 在所有 Python3 提交中击败了73.32% 的用户
内存消耗：15.8 MB, 在所有 Python3 提交中击败了9.06% 的用户
通过测试用例：88 / 88

```python
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        # 还是先傻逼写法
        s = None
        e = None
        for i in range(len(nums)):
            if nums[i] == target:
                if s == None:
                    s = i
                else:
                    e = i
            else:
                if s:
                    break

        if s != None:
            return [s, e if e else s]
        else:
            return [-1, -1]

```
**改进**
两次二分，分别查找左右边界，对于左边界中间值向下取整，对于有边界，中间值向上取整

- 执行用时：28 ms, 在所有 Python3 提交中击败了90.91% 的用户
内存消耗：15.8 MB, 在所有 Python3 提交中击败了25.76% 的用户
通过测试用例：88 / 88

```python
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        s, e, m = None, None, 0
        l, r = 0, len(nums) - 1
        if r < 0:
            return [-1, -1]
        while l < r:
            m = (l + r) // 2
            if nums[m] > target:
                r = m - 1
            elif nums[m] == target:
                r = m
            else:
                l = m + 1
        if nums[l] != target:
            return [-1, -1]
        s = l

        r = len(nums) - 1
        while l < r:
            m = int(l + (r - l + 1) / 2)
            if nums[m] > target:
                r = m - 1
            elif nums[m] == target:
                l = m
            else:
                l = m + 1
        return [s, l]
```

**改进**
二分，注意 在有序的排列里二分才有意义，而且两边一定有一边是有序的

- 执行用时：32 ms, 在所有 Python3 提交中击败了68.16% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了86.65% 的用户
通过测试用例：

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        # 肯定是二分法，学习一下二分法
        l, r = 0, len(nums) - 1
        while l <= r:
            m = (l + r) // 2
            if nums[m] == target:
                return m
            if nums[l] <= nums[m]:  # 只能在有序的排列里找才有意义，所以要先找到有序的排列
                if nums[l] <= target < nums[m]:
                    r = m - 1
                else:
                    l = m + 1
            else:
                if nums[m] < target <= nums[r]:
                    l = m + 1
                else:
                    r = m - 1
        return -1

```
**Tag: 数组、二分查找**

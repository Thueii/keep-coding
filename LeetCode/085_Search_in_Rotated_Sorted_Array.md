# 搜索旋转排序数组

Link => [搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)

## 题目
整数数组 nums 按升序排列，数组中的值 互不相同 。

在传递给函数之前，nums 在预先未知的某个下标 k（0 <= k < nums.length）上进行了 旋转，使数组变为 [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]（下标 从 0 开始 计数）。例如， [0,1,2,4,5,6,7] 在下标 3 处经旋转后可能变为 [4,5,6,7,0,1,2] 。

给你 旋转后 的数组 nums 和一个整数 target ，如果 nums 中存在这个目标值 target ，则返回它的下标，否则返回 -1 。

**示例1**

    输入：nums = [4,5,6,7,0,1,2], target = 0
    输出：4

**示例2**

    输入：nums = [4,5,6,7,0,1,2], target = 3
    输出：-1

**进阶**
进阶：你可以设计一个时间复杂度为 O(log n) 的解决方案吗？

**执行结果：通过 显示详情**
弱智写法，先过再说

- 执行用时：36 ms, 在所有 Python3 提交中击败了37.48% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了88.75% 的用户
通过测试用例：195 / 195

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        if target in nums:
            return nums.index(target)
        else:
            return -1
```
**改进**
直接赋值该位置，再赋值0

- 执行用时：32 ms, 在所有 Python3 提交中击败了98.22% 的用户
内存消耗：15.5 MB, 在所有 Python3 提交中击败了28.25% 的用户
通过测试用例：74 / 74

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        # 双指针
        j = 0
        for i in range(len(nums)):
            if nums[i]:
                nums[j] = nums[i]
                j += 1
        for i in range(j, len(nums)):
            nums[i] = 0
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

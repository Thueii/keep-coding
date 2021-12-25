# 移动零

Link => [移动零](https://leetcode-cn.com/problems/move-zeroes/)

## 题目
给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

**示例1**
>输入：[0,1,0,3,12]<br />
>输出：[1,3,12,0,0]<br />
>解释："a" 无法匹配 "aa" 整个字符串。<br />

**说明**
1. 必须在原数组上操作，不能拷贝额外的数组。
2. 尽量减少操作次数。

**执行结果：通过 显示详情**
确实感觉没什么技巧，写的很慢吧

- 执行用时：212 ms, 在所有 Python3 提交中击败了24.95% 的用户
内存消耗：15.4 MB, 在所有 Python3 提交中击败了82.77% 的用户
通过测试用例：74 / 74

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        num = 0
        p = 0
        while p < len(nums):
            if nums[p] == 0:
                nums.pop(p)
                num += 1
            else:
                p += 1
        for i in range(num):
            nums.append(0)
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

**Tag: 数组、双指针**

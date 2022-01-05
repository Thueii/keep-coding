# 下一个排列

Link => [下一个排列](https://leetcode-cn.com/problems/next-permutation/)

## 题目
实现获取 下一个排列 的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列（即，组合出下一个更大的整数）。

如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。

必须 原地 修改，只允许使用额外常数空间。

**示例1**

    输入：nums = [1,2,3]
    输出：[1,3,2]

**示例2**

    输入：nums = [3,2,1]
    输出：[1,2,3]

**示例3**

    输入：nums = [1,1,5]
    输出：[1,5,1]


**执行结果：通过 显示详情**
我变强了。。。。

- 执行用时：24 ms, 在所有 Python3 提交中击败了96.68% 的用户
内存消耗：14.9 MB, 在所有 Python3 提交中击败了78.27% 的用户
通过测试用例：265 / 265
```python
class Solution:
    def nextPermutation(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        max_idx = len(nums) - 1
        min_idx = len(nums) - 1

        for i in range(len(nums)-1, -1, -1):
            if nums[i] < nums[max_idx]:
                for j in range(len(nums[max_idx:])):
                    if nums[i] >= nums[max_idx + j]:
                        break
                    else:
                        tmp = max_idx + j
                nums[tmp], nums[i] = nums[i], nums[tmp]
                nums[i+1:] = nums[i+1:][::-1]
                break
            else:
                max_idx = i
        else:
            if max_idx == 0:
                nums.sort()
            else:
                nums[0], nums[max_idx] = nums[max_idx], nums[0]
                nums[1:] = nums[1:][::-1]
```
**Tag: 数组、双指针**
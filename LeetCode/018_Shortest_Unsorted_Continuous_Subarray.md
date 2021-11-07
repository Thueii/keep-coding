# 最短无序连续子数组

Link => [最短无序连续子数组](https://leetcode-cn.com/problems/shortest-unsorted-continuous-subarray/)

给你一个整数数组 nums ，你需要找出一个 连续子数组 ，如果对这个子数组进行升序排序，那么整个数组都会变为升序排序。

请你找出符合题意的 最短 子数组，并输出它的长度。

>输入：nums = [2,6,4,8,10,9,15]<br />
>输出：5<br />

>输入：nums = [1,2,3,4]<br />
>输出：0<br />

执行结果：
通过
显示详情

添加备注
执行用时：44 ms, 在所有 Python3 提交中击败了94.15% 的用户
内存消耗：15.8 MB, 在所有 Python3 提交中击败了34.36% 的用户
通过测试用例：307 / 307

```python
class Solution:
    def findUnsortedSubarray(self, nums: List[int]) -> int:
        # 俺来也
        # 写完了才发现这样只维护了最右边的不合理的点，而无法确定左边的边界
        # 比如说[1, 2, 4, 5, 3]从左往右只能知道3是不合理的，而无法判定左边的不合理位置
        # 以下是错的
        # stack = []
        # stack2 = []
        # index = 0
        # flag = 0
        # target = -float(inf)
        # while index < len(nums):
        #     if index == 0:
        #         target = nums[index]
        #         index += 1
        #     else:
        #         if nums[index] > target:
        #             target = nums[index]
        #             stack2 = []
        #             index += 1
        #             flag = 2
        #         elif nums[index] == target:
        #             stack2.append(index)
        #             index += 1
        #             flag = 1
        #         else:
        #             stack += stack2
        #             stack.append(index)
        #             stack2 = []
        #             flag = 2
        #             index += 1
        # if not stack:
        #     return 0
        # return max(stack)-min(stack) + 2
        # 以上都是错的
        m = -inf
        end = -1
        for i in range(len(nums)):
            if nums[i] > m:
                m = nums[i]
            elif nums[i] < m:
                end = i
        if end == -1:
            return 0

        n = inf
        start = len(nums)
        for i in range(len(nums)-1, -1, -1):
            if nums[i] < n:
                n = nums[i]
            elif nums[i] > n:
                start = i
        return end - start + 1

```
**Tag: 栈、贪心、数组、双指针、排序、单调栈**

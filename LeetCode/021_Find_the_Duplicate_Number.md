# 寻找重复数

Link => [寻找重复数](https://leetcode-cn.com/problems/find-the-duplicate-number/)
给定一个包含 n + 1 个整数的数组 nums ，其数字都在 1 到 n 之间（包括 1 和 n），可知至少存在一个重复的整数。

假设 nums 只有 一个重复的整数 ，找出 这个重复的数 。

你设计的解决方案必须不修改数组 nums 且只用常量级 O(1) 的额外空间。


>输入：nums = [1,3,4,2,2]<br />
>输出：2<br />

>输入：nums = [3,1,3,4,2]<br />
>输出：3<br />

执行结果：
通过
显示详情

添加备注
执行用时：72 ms, 在所有 Python3 提交中击败了95.57% 的用户
内存消耗：31.9 MB, 在所有 Python3 提交中击败了5.46% 的用户
通过测试用例：58 / 58

```python
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        return int((sum(nums) - sum(set(nums)))/(len(nums)-len(set(nums))))
```
改进：
二分法，充分利用题意

执行结果：
通过
显示详情

添加备注
执行用时：316 ms, 在所有 Python3 提交中击败了24.47% 的用户
内存消耗：25.6 MB, 在所有 Python3 提交中击败了81.94% 的用户
通过测试用例：58 / 58
```python
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        left = 1
        right = len(nums) - 1
        while(left<right):
            mid=(left+right)//2
            count=0
            for num in nums:
                if(num<=mid):
                    count+=1
            if(count<=mid):
                left=mid+1
            else:
                right=mid
        return left
```
**Tag: 位运算、数组、双指针、二分查找**

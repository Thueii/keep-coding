# 两数之和

Link => [两数之和](https://leetcode-cn.com/problems/two-sum/)

**题目：给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。你可以按任意顺序返回答案。**

> 示例 1：<br />
> 输入：nums = [2,7,11,15], target = 9<br />
> 输出：[0,1]<br />
> 解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。<br />
>
> 示例 2： <br />
> 输入：nums = [3,2,4], target = 6<br />
> 输出：[1,2]<br />
>
> 示例 3： <br />
> 输入：nums = [3,3], target = 6<br />
> 输出：[0,1]<br />

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        adict = {}
        for i in range(len(nums)):
            if target-nums[i] in adict:
                return [adict[target-nums[i]], i]
            adict[nums[i]] = i
```

**Tag: 数组、哈希**

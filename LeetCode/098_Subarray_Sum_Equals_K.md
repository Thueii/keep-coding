# 和为 K 的子数组

Link => [和为 K 的子数组](https://leetcode-cn.com/problems/subarray-sum-equals-k/)

## 题目

    给你一个整数数组 nums 和一个整数 k ，请你统计并返回该数组中和为 k 的连续子数组的个数。

**示例1**

    输入：nums = [1,1,1], k = 2
    输出：2

**示例2**

    输入：nums = [1,2,3], k = 3
    输出：2

**执行结果：通过 显示详情**
全排列，就是超时，没毛病

- 超时

```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        count = 0
        for i in range(len(nums)):
            for j in range(i, len(nums)):
                if sum(nums[i:j+1]) == k: count+=1
        return count
```
**改进**
基础升级版，前缀和，好理解，但是还是慢，是从当前往后算的思路

- 超时

```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        count = 0
        pre = [0] * (len(nums)+1)
        for i in range(1, len(nums)+1):
            pre[i] = pre[i-1] + nums[i-1]

        for i in range(1, len(nums)+1):
            for j in range(i, len(nums)+1):
                if pre[j] - pre[i-1] == k: count += 1
        return count
```
**改进**
当前往前的思路，前缀和+哈希表，巧妙

- 执行用时：64 ms, 在所有 Python3 提交中击败了92.43% 的用户
内存消耗：17.2 MB, 在所有 Python3 提交中击败了36.62% 的用户
通过测试用例：89 / 89

```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        count = {}
        all_sum = 0
        res = 0
        for num in nums:
            all_sum += num
            if all_sum == k:
                res += 1
            if all_sum - k in count:
                res += count[all_sum-k]
            count[all_sum] = count.get(all_sum, 0) + 1
        return res
```
**Tag: 数组、哈希表、前缀和**

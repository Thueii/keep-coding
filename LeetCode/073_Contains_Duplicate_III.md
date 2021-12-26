# 存在重复元素 III

Link => [存在重复元素 III](https://leetcode-cn.com/problems/contains-duplicate-iii/)

## 题目
给你一个整数数组 nums 和两个整数 k 和 t 。请你判断是否存在 两个不同下标 i 和 j，使得 abs(nums[i] - nums[j]) <= t ，同时又满足 abs(i - j) <= k 。

如果存在则返回 true，不存在返回 false。

**示例1**
>输入：nums = [1,2,3,1], k = 3, t = 0<br />
>输出：true<br />

**示例2**
>输入：nums = [1,0,1,1], k = 1, t = 2<br />
>输出：true<br />

**执行结果：通过 显示详情**
料到了

- 超出时间限制

```python
class Solution:
    def containsNearbyAlmostDuplicate(self, nums: List[int], k: int, t: int) -> bool:
        adict = {}
        for idx in range(len(nums)):
            num = nums[idx]
            if num not in adict:
                adict[num] = [idx]
            else:
                adict[num].append(idx)

            num_low = num-t
            num_high = num+t
            for i in adict.keys():
                if num_low <= i <= num_high: 
                    for each_id in adict[i]:
                        if each_id != idx and abs(each_id - idx) <= k:
                            return True
        return False
```

**改进**
桶排序，相当牛逼，用桶来做到元素差小于t，用k之前的元素的桶的方式来保证索引在区间内，而且每个桶只需要存一个元素，两个元素就直接返回了

- 执行用时：40 ms, 在所有 Python3 提交中击败了97.72% 的用户
内存消耗：17.3 MB, 在所有 Python3 提交中击败了63.86% 的用户
通过测试用例：53 / 53

```python
class Solution:
    def containsNearbyAlmostDuplicate(self, nums: List[int], k: int, t: int) -> bool:
        if t < 0 or k < 0:
            return False
        all_buckets = {}
        bucket_size = t + 1
        for i in range(len(nums)):
            bucket_num = nums[i] // bucket_size
            if bucket_num in all_buckets:
                return True
            all_buckets[bucket_num] = nums[i] # 只用一个元素
            if (bucket_num - 1) in all_buckets and abs(all_buckets[bucket_num - 1] - nums[i]) <= t: # 检查前一个桶
                return True
            if (bucket_num + 1) in all_buckets and abs(all_buckets[bucket_num + 1] - nums[i]) <= t: # 检查后一个桶
                return True
            if i >= k:
                all_buckets.pop(nums[i-k]//bucket_size) # 其实是去掉num[i-k]这个元素，因为超过索引范围
        return False
```
**Tag: 数组、哈希表、滑动窗口**

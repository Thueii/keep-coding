# 存在重复元素 II

Link => [存在重复元素 II](https://leetcode-cn.com/problems/contains-duplicate-ii/)

## 题目
给定一个整数数组和一个整数 k，判断数组中是否存在两个不同的索引 i 和 j，使得 nums [i] = nums [j]，并且 i 和 j 的差的 绝对值 至多为 k。

**示例1**
>输入：nums = [1,2,3,1], k = 3<br />
>输出：true<br />

**示例2**
>输入：nums = [1,0,1,1], k = 1<br />
>输出：true<br />

**执行结果：通过 显示详情**
可以把吧

- 执行用时：60 ms, 在所有 Python3 提交中击败了96.68% 的用户
内存消耗：26 MB, 在所有 Python3 提交中击败了23.44% 的用户
通过测试用例：51 / 51

```python
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        adict = {}
        for idx in range(len(nums)):
            num = nums[idx]
            if num in adict and idx - adict[num] <= k:
                return True
            adict[num] = idx
        return False
```
**Tag: 数组、哈希表、滑动窗口**

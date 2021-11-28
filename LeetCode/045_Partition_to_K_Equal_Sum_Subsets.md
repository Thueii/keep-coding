# 划分为k个相等的子集

Link => [划分为k个相等的子集](https://leetcode-cn.com/problems/partition-to-k-equal-sum-subsets/)

## 题目
给定一个整数数组  nums 和一个正整数 k，找出是否有可能把这个数组分成 k 个非空子集，其总和都相等。

**示例1**
>输入：nums = [4, 3, 2, 3, 5, 2, 1], k = 4<br />
>输出：True<br />
>说明：有可能将其分成 4 个子集（5），（1,4），（2,3），（2,3）等于总和。<br />

**执行结果：通过 显示详情**

主要是敢想。。。有时候不敢想，总觉得很复杂，要想到这个dfs究竟做什么!这一题就想着这个dfs就做当前篮筐和情况是否能满足

- 执行用时：32 ms, 在所有 Python3 提交中击败了96.90% 的用户
内存消耗：15 MB, 在所有 Python3 提交中击败了54.99% 的用户
通过测试用例：142 / 142

```python
class Solution:
    def canPartitionKSubsets(self, nums: List[int], k: int) -> bool:
        if k == 1:
            return True
        tar = sum(nums) / k
        if tar != int(tar):
            return False
        def dfs(group):
            # 当前篮筐是否可以
            if not nums:
                return True 
                # 放完了其实是个true，因为sum和k的限制
                # 不会是你想的空出来的情况，只能是塞得满满当当才对
            cur = nums.pop()
            for i in range(k):
                if group[i] + cur <= tar:
                    group[i] += cur
                    if dfs(group):
                        return True
                    else:
                        group[i] -= cur
                if group[i] == 0:
                    break
            nums.append(cur)
            return False

        nums.sort()
        return dfs([0] * k)
```

**Tag: 记忆化搜索、位运算、动态规划、状态压缩、回溯、数组**

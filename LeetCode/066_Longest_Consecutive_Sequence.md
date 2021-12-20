# 最长连续序列

Link => [最长连续序列](https://leetcode-cn.com/problems/longest-consecutive-sequence/)

## 题目
给定一个未排序的整数数组 nums ，找出数字连续的最长序列（不要求序列元素在原数组中连续）的长度。

请你设计并实现时间复杂度为 O(n) 的算法解决此问题。

**示例1**
>输入：nums = [100,4,200,1,3,2]<br />
>输出：4<br />
>解释：最长数字连续序列是 [1, 2, 3, 4]。它的长度为 4。<br />

**示例2**
>输入：nums = [0,3,7,2,5,8,4,6,0,1]<br />
>输出：9<br />

**执行结果：通过 显示详情**
写出来了，但完全没写出来

- 超出时间限制

```python
class UnionFind:
    def __init__(self):
        self.father= {}

    def add(self, x):
        if x not in self.father:
            self.father[x] = None

    def find(self, x):
        if x in self.father and not self.father[x]:
            self.father[x] = self.find(x-1)
            return self.father[x]
        elif x not in self.father:
            return x + 1
        else:
            return self.father[x]

class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        if not nums:
            return 0
        res = 1

        uf = UnionFind()
        for i in nums:
            uf.add(i)
        for i in nums:
            value = uf.find(i)
            res = max(res, i-value+1)
        return res
```
**改进**
简单方法

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        nums = set(nums)
        res = 0
        for i in nums:
            # 只找每个片段开头
            if i-1 not in nums:
                j = i+1
                # 计算每个片段长度
                while j in nums:
                    j += 1
                res = max(res,j-i)
        return res
```

**改进**

**Tag: 并查集、数组、哈希表**

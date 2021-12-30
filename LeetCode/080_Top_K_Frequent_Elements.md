# 前 K 个高频元素

Link => [前 K 个高频元素](https://leetcode-cn.com/problems/top-k-frequent-elements/)

## 题目
给你一个整数数组 nums 和一个整数 k ，请你返回其中出现频率前 k 高的元素。你可以按 任意顺序 返回答案。

**示例1**

    输入: nums = [1,1,1,2,2,3], k = 2
    输出: [1,2]

**示例2**

    输入: nums = [1], k = 1
    输出: [1]

**执行结果：通过 显示详情**
基本方法

    时间复杂度：O(nlogn)
    空间复杂度：O(n)


- 执行用时：36 ms, 在所有 Python3 提交中击败了87.82% 的用户
内存消耗：17.7 MB, 在所有 Python3 提交中击败了19.27% 的用户
通过测试用例：21 / 21

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        adict = collections.defaultdict(int)
        for i in nums:
            adict[i] += 1
        dict_list = sorted(adict.items(), key=lambda x:x[1], reverse=True)
        res = []

        return [dict_list[i][0] for i in range(k)]
```
**改进：**
黑魔法？？？？？

- 执行用时：40 ms, 在所有 Python3 提交中击败了72.16% 的用户
内存消耗：17.5 MB, 在所有 Python3 提交中击败了92.06% 的用户
通过测试用例：21 / 21
```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = collections.Counter(nums)
        return [item[0] for item in count.most_common(k)]
```
**改进：**

    时间复杂度：O(nlogk)
    空间复杂度：O(n)


- 执行用时：36 ms, 在所有 Python3 提交中击败了87.82% 的用户
内存消耗：17.6 MB, 在所有 Python3 提交中击败了51.40% 的用户
通过测试用例：21 / 21

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = collections.Counter(nums)
        heap = []
        for key, val in count.items():
            if len(heap) >= k:
                if val > heap[0][0]:
                    heapq.heapreplace(heap, (val, key))
            else:
                heapq.heappush(heap, (val, key))
        return [item[1] for item in heap]
```
**改进：**

    时间复杂度：平均O(n)
    空间复杂度：O(n)



- 执行用时：28 ms, 在所有 Python3 提交中击败了99.03% 的用户
内存消耗：17.8 MB, 在所有 Python3 提交中击败了13.97% 的用户
通过测试用例：21 / 21

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = collections.Counter(nums)
        num_cnt = list(count.items())
        topKs = self.findTopK(num_cnt, k, 0, len(num_cnt) - 1)
        return [item[0] for item in topKs]
    
    def findTopK(self, num_cnt, k, low, high):
        pivot = random.randint(low, high)
        num_cnt[low], num_cnt[pivot] = num_cnt[pivot], num_cnt[low]
        base = num_cnt[low][1]
        i = low
        for j in range(low + 1, high + 1):
            if num_cnt[j][1] > base:
                num_cnt[i + 1], num_cnt[j] = num_cnt[j], num_cnt[i + 1]
                i += 1
        num_cnt[low], num_cnt[i] = num_cnt[i], num_cnt[low]
        if i == k - 1:
            return num_cnt[:k]
        elif i > k - 1:
            return self.findTopK(num_cnt, k, low, i - 1)
        else:
            return self.findTopK(num_cnt, k, i + 1, high)


```
**Tag: 数组、哈希表、分治、桶排序、计数、快速选择、排序、堆**

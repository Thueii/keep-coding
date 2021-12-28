# 多数元素

Link => [多数元素](https://leetcode-cn.com/problems/majority-element/)

## 题目
给定一个大小为 n 的数组，找到其中的多数元素。多数元素是指在数组中出现次数 大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

**进阶**
尝试设计时间复杂度为 O(n)、空间复杂度为 O(1) 的算法解决此问题。<br />

**示例1**

    输入：[3,2,3]
    输出：3

**示例2**

    输入：[2,2,1,1,1,2,2]
    输出：2

**执行结果：通过 显示详情**
原始的很

- 执行用时：44 ms, 在所有 Python3 提交中击败了46.05% 的用户
内存消耗：16.2 MB, 在所有 Python3 提交中击败了14.84% 的用户
通过测试用例：47 / 47

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        adict = collections.defaultdict(int)
        length = int(len(nums) / 2)
        max_num = 0
        for i in nums:
            adict[i] += 1
            if adict[i] > length:
                return i
```

**改进**
但是感觉不是O（n）啊

- 执行用时：36 ms, 在所有 Python3 提交中击败了84.38% 的用户
内存消耗：16.1 MB, 在所有 Python3 提交中击败了62.10% 的用户
通过测试用例：47 / 47

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        nums.sort()
        return nums[len(nums)//2]
```

**改进**
[摩尔投票法](https://leetcode-cn.com/problems/majority-element/solution/duo-shu-yuan-su-by-leetcode-solution/)

- 执行用时：24 ms, 在所有 Python3 提交中击败了99.78% 的用户
内存消耗：16 MB, 在所有 Python3 提交中击败了90.03% 的用户
通过测试用例：47 / 47

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        maj = None
        count = 0
        for i in nums:
            if i == maj:
                count += 1
            elif count == 0:
                maj = i
                count += 1
            else:
                count -= 1
        return maj
```
**Tag: 数组、哈希表、分治、计数、排序**

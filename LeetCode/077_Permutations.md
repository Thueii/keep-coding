# 全排列

Link => [全排列](https://leetcode-cn.com/problems/permutations/)

## 题目
给定一个不含重复数字的数组 nums ，返回其 所有可能的全排列 。你可以 按任意顺序 返回答案。

**示例1**

    输入：nums = [1,2,3]
    输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

**示例2**

    输入：nums = [0,1]
    输出：[[0,1],[1,0]]

**执行结果：通过 显示详情**
不太熟这个

- 执行用时：60 ms, 在所有 Python3 提交中击败了9.35% 的用户
内存消耗：15.2 MB, 在所有 Python3 提交中击败了18.83% 的用户
通过测试用例：26 / 26

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        res = []
        def dfs(pre_list, nums):
            tmp = copy.deepcopy(pre_list)
            if not nums:
                res.append(tmp)
                return
            for i in range(len(nums)):
                tmp = copy.deepcopy(pre_list)
                anum = nums.pop(i)
                pre_list.append(anum)
                dfs(pre_list, nums)
                pre_list = tmp
                nums.insert(i, anum)
            return

        dfs([], nums)
        return res
```

**改进**
改进了一点点

- 执行用时：40 ms, 在所有 Python3 提交中击败了23.91% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了66.18% 的用户
通过测试用例：26 / 26

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        res = []
        length = len(nums)
        def dfs(pre_list, nums):
            if not nums:
                res.append(copy.deepcopy(pre_list))
                return
            for i in range(len(nums)):
                anum = nums.pop(i)
                pre_list.append(anum)
                dfs(pre_list, nums)
                pre_list.pop()
                nums.insert(i, anum)
            return

        dfs([], nums)
        return res
```
**改进**
原来[:]就是拷贝一份。。。。用深拷贝好他妈浪费时间啊，进步了这么多

- 执行用时：32 ms, 在所有 Python3 提交中击败了78.52% 的用户
内存消耗：15 MB, 在所有 Python3 提交中击败了80.57% 的用户
通过测试用例：26 / 26

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        res = []
        def dfs(pre_list, nums):
            if not nums:
                res.append(pre_list[:])
                return
            for i in range(len(nums)):
                anum = nums.pop(i)
                pre_list.append(anum)
                dfs(pre_list, nums)
                pre_list.pop()
                nums.insert(i, anum)
            return

        dfs([], nums)
        return res
```
**改进**
这是魔法

- 执行用时：32 ms, 在所有 Python3 提交中击败了78.52% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了70.48% 的用户
通过测试用例：26 / 26

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        return list(itertools.permutations(nums))

```
**改进**
数组拼接，不用恢复状态，但是感觉比较慢，但是很清晰

- 执行用时：36 ms, 在所有 Python3 提交中击败了53.32% 的用户
内存消耗：15.2 MB, 在所有 Python3 提交中击败了35.30% 的用户
通过测试用例：26 / 26

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        res = []
        def dfs(pre_list, nums):
            if not nums:
                res.append(pre_list[:])
                return
            for i in range(len(nums)):
                dfs(pre_list+[nums[i]], nums[:i]+nums[i+1:])
            return

        dfs([], nums)
        return res
```
**Tag: 数组、回溯**

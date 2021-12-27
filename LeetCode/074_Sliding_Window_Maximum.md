# 滑动窗口最大值

Link => [滑动窗口最大值](https://leetcode-cn.com/problems/sliding-window-maximum/)

## 题目
给你一个整数数组 nums，有一个大小为 k 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 k 个数字。滑动窗口每次只向右移动一位。

返回滑动窗口中的最大值。

**示例1**
>输入：nums = [1,3,-1,-3,5,3,6,7], k = 3<br />
>输出：[3,3,5,5,6,7]<br />
>说明：<br />
滑动窗口的位置                最大值<br />
---------------               -----<br />
[1  3  -1] -3  5  3  6  7       3<br />
 1 [3  -1  -3] 5  3  6  7       3<br />
 1  3 [-1  -3  5] 3  6  7       5<br />
 1  3  -1 [-3  5  3] 6  7       5<br />
 1  3  -1  -3 [5  3  6] 7       6<br />
 1  3  -1  -3  5 [3  6  7]      7<br />

**执行结果：通过 显示详情**
太不容易了，想了半天用单调栈，但是感觉处理超过窗口的那部分处理的不好

- 执行用时：3768 ms, 在所有 Python3 提交中击败了22.34% 的用户
内存消耗：27.6 MB, 在所有 Python3 提交中击败了33.36% 的用户
通过测试用例：61 / 61

```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        res_list = []
        stack = []
        p = []
        for i in range(k):
            num = nums[i]
            while stack:
                if stack[-1] > num:
                    break
                stack.pop()
                p.pop()
            stack.append(num)
            p.append(i)

        res_list.append(stack[0])

        start = 0
        for i in range(k, len(nums)):
            start += 1
            
            num = nums[i]
            while stack:
                if stack[-1] > num:
                    break
                stack.pop()
                p.pop()
            stack.append(num)
            p.append(i)

            while p[0] < start:
                p.pop(0)
                stack.pop(0)
            res_list.append(stack[0])
                
        return res_list
```

**改进**
少pop一次试一试，好了一丢丢

- 执行用时：2012 ms, 在所有 Python3 提交中击败了29.65% 的用户
内存消耗：27.8 MB, 在所有 Python3 提交中击败了28.60% 的用户
通过测试用例：61 / 61

```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        res_list = []
        stack = []
        p = []
        for i in range(k):
            num = nums[i]
            while stack:
                if stack[-1] > num:
                    break
                stack.pop()
                p.pop()
            stack.append(num)
            p.append(i)

        res_list.append(stack[0])

        start = 0
        for i in range(k, len(nums)):
            start += 1
            
            num = nums[i]
            while stack and p:
                if stack[-1] > num:
                    break
                stack.pop()
                p.pop()
            stack.append(num)
            p.append(i)

            while p[0] < start:
                p.pop(0)
            res_list.append(nums[p[0]])
                
        return res_list
```
**改进**
双端队列，没有遇到过，正好好好看看

- 执行用时：264 ms, 在所有 Python3 提交中击败了99.54% 的用户
内存消耗：27.1 MB, 在所有 Python3 提交中击败了50.92% 的用户
通过测试用例：61 / 61

```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        res_list = []
        stack = deque()

        for i in range(k):
            num = nums[i]
            while stack and stack[-1] < num:  # 相等的也记录 后面有用
                stack.pop()
            stack.append(num)

        res_list.append(stack[0])

        start = 0
        for i in range(k, len(nums)):
            start += 1
            num = nums[i]
            while stack and stack[-1] < num:
                stack.pop()
            stack.append(num)

            if stack[0] == nums[start-1]:  # 因为这里相等的会记录索引小的，所以可以用这一点来判断是否是前一个！太妙了
                stack.popleft()
            res_list.append(stack[0])
                
        return res_list
```
**Tag: 数组、哈希表、滑动窗口**

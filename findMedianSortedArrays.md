# 寻找两个正序数组的中位数

Link => [寻找两个正序数组的中位数
](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/)

**题目：给定两个大小分别为 m 和 n 的正序（从小到大）数组 nums1 和 nums2。请你找出并返回这两个正序数组的 中位数 。**
>示例1：<br />
>输入：nums1 = [1,3], nums2 = [2]<br />
>输出：2.00000<br />
>解释：合并数组 = [1,2,3] ，中位数 2<br />
> 
> 示例 2：<br />
> 输入：nums1 = [1,2], nums2 = [3,4]<br />
> 输出：合并数组 = [1,2,3,4] ，中位数 (2 + 3) / 2 = 2.5<br />
> 
> 示例 3：<br />
> 输入：nums1 = [0,0], nums2 = [0,0]<br />
> 输出：0.00000<br />

```python
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        m, n = len(nums1), len(nums2)
        if m > n:
            return self.findMedianSortedArrays(nums2, nums1)
        if m == 0:
            if n%2:
                return nums2[n//2]
            else:
                return (nums2[n//2]+nums2[n//2 - 1])/2
        if n == 0:
            if m%2:
                return nums1[m//2]
            else:
                return (nums1[m//2]+nums1[m//2 - 1])/2
        up = (m+1)//2 
        down = (m+n)//2 - up 
        left = 0
        right = m
        while True:
            if up == m:
                if nums1[up-1]>nums2[down]:
                    temp = up
                    up = left + (up+1-left)//2
                    if temp == up:
                        up -= 1
                    right = temp
                    down = (m+n)//2 - up
                    continue
                else:
                    break
            if up == 0:
                if nums1[up] < nums2[down-1]:
                    temp = up
                    up = up + (right+1-up)//2
                    left = temp
                    down = (m+n)//2 - up
                    continue
                else:
                    break
            if max(nums1[up-1], nums2[down-1]) <= min(nums1[up], nums2[down]):
                break
            if nums1[up] < nums2[down-1]:
                temp = up
                up = up + (right+1-up)//2
                left = temp
                down = (m+n)//2 - up
            elif nums1[up-1] > nums2[down]:
                temp = up
                up = left + (up+1-left)//2
                if temp == up:
                    up -= 1
                right = temp
                down = (m+n)//2 - up

        if (m+n)%2:
            if up == m:
                return nums2[down]
            elif up == 0:
                return min(nums1[up], nums2[down])
            else:
                return min(nums1[up],nums2[down])
        else:
            if up == m:
                if down != 0:
                    return (max(nums1[up-1], nums2[down-1]) + nums2[down])/2
                else:
                    return (nums1[up-1]+nums2[0])/2
            elif up == 0:
                if down != n:
                    return (nums2[down-1] + min(nums1[up], nums2[down]))/2
                else:
                    return (nums2[down-1] + nums1[0])/2
            else:
                return (max(nums1[up-1],nums2[down-1])+min(nums1[up],nums2[down]))/2
```

**Tag: 数组、二分查找、分治**

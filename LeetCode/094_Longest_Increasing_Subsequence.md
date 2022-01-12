# 最长递增子序列

Link => [最长递增子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence/)

## 题目

    给你一个整数数组 nums ，找到其中最长严格递增子序列的长度。

    子序列是由数组派生而来的序列，删除（或不删除）数组中的元素而不改变其余元素的顺序。例如，[3,6,2,7] 是数组 [0,3,1,6,2,2,7] 的子序列。

**示例1**

    输入：nums = [10,9,2,5,3,7,101,18]
    输出：4
    解释：最长递增子序列是 [2,3,7,101]，因此长度为 4 。

**示例2**

    输入：nums = [0,1,0,3,2,3]
    输出：4

**执行结果：通过 显示详情**
感觉在后面每一个都要找一下有点慢呢？但是好像又不得不找？这是N^2的复杂度，总感觉不太对，但是打败人数还算是可以。。

- 执行用时：2580 ms, 在所有 Python3 提交中击败了63.57% 的用户
内存消耗：15.5 MB, 在所有 Python3 提交中击败了5.10% 的用户
通过测试用例：54 / 54

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        dp = [1] * len(nums)
        stack = []

        for i in range(len(nums)-1, -1, -1):
            if stack:
                tmp = 0
                for each in stack[::-1]:
                    if each[0] > nums[i]:
                        tmp = max(tmp, dp[each[1]])
                dp[i] = tmp + 1
                        
            stack.append([nums[i], i])
        return max(dp)
```

**另外的**
这题好像没有设么别的办法了，下面有一种用二进制算的 很巧妙，但是枚举了所有组合，很费时间，只能算是一种思路吧
[分享一个不用动态规划，采用二进制思路的方法](https://leetcode-cn.com/problems/maximal-square/solution/fen-xiang-yi-ge-bu-yong-dong-tai-gui-hua-cai-yong-/)
```python
class Solution:
    def getWidth(self,num):  #步骤3：求一个数中连续最多的1
        w=0
        while num>0:
            num&=num<<1
            w+=1
        return w
    def maximalSquare(self, matrix: List[List[str]]) -> int:
        nums=[int(''.join(n),base=2) for n in matrix]  #步骤1：每一行当作二进制数
        res,n=0,len(nums)
        for i in range(n):   #步骤2：枚举所有的组合，temp存储相与的结果
            temp=nums[i]
            for j in range(i,n):
                temp&=nums[j]
                w=self.getWidth(temp)
                h=j-i+1
                res=max(res,min(w,h))
        return res*res
```
**Tag: 数组、动态规划、矩阵**

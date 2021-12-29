# 除自身以外数组的乘积

Link => [除自身以外数组的乘积](https://leetcode-cn.com/problems/product-of-array-except-self/)

## 题目
给你一个长度为 n 的整数数组 nums，其中 n > 1，返回输出数组 output ，其中 output[i] 等于 nums 中除 nums[i] 之外其余各元素的乘积。

**示例1**

    输入: [1,2,3,4]
    输出: [24,12,8,6]

**提示**
题目数据保证数组之中任意元素的全部前缀元素和后缀（甚至是整个数组）的乘积都在 32 位整数范围内。

**说明** 
请不要使用除法，且在 O(n) 时间复杂度内完成此题。

**进阶**
你可以在常数空间复杂度内完成这个题目吗？（ 出于对空间复杂度分析的目的，输出数组不被视为额外空间。）

**执行结果：通过 显示详情**
比较基础的一个写法。。。O(n)

- 执行用时：56 ms, 在所有 Python3 提交中击败了87.06% 的用户
内存消耗：21 MB, 在所有 Python3 提交中击败了13.58% 的用户
通过测试用例：20 / 20

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        leftmul = []
        rightmul = []
        leftres = 1
        rightres = 1

        for i in nums:
            leftres *= i
            leftmul.append(leftres)
        for i in nums[::-1]:
            rightres *= i
            rightmul.append(rightres)

        rightmul = rightmul[::-1]

        res = [rightmul[1]]

        for i in range(1, len(nums)-1):
            tmp = leftmul[i-1] * rightmul[i+1]
            res.append(tmp)

        res.append(leftmul[-2])
        return res
```
**改进：**
O(1)空间复杂度，没啥就是利用一下本身而已，思考一下错位就很好了。

- 执行用时：44 ms, 在所有 Python3 提交中击败了99.61% 的用户
内存消耗：19.7 MB, 在所有 Python3 提交中击败了53.65% 的用户
通过测试用例：20 / 20
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        res = []
        p = 1
        for i in nums:
            p *= i
            res.append(p)
        q = nums[-1]
        res[-1] = res[-2]
        for i in range(len(nums)-2, 0, -1):
            res[i] = res[i-1] * q
            q *= nums[i]
        res[0] = q
        return res
        
```

**Tag: 数组、前缀和**

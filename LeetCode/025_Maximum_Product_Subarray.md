# 乘积最大子数组

Link => [乘积最大子数组](https://leetcode-cn.com/problems/maximum-product-subarray/)
给你一个整数数组 nums ，请你找出数组中乘积最大的连续子数组（该子数组中至少包含一个数字），并返回该子数组所对应的乘积。

>输入: [2,3,-2,4]<br />
>输出: 6<br />
>解释: 子数组 [2,3] 有最大乘积 6。<br />

>输入: [-2,0,-1]<br />
>输出: 0<br />
>解释: 结果不能为 2, 因为 [-2,-1] 不是子数组。<br />

执行结果：
通过
显示详情

添加备注
执行用时：36 ms, 在所有 Python3 提交中击败了83.34% 的用户
内存消耗：15.7 MB, 在所有 Python3 提交中击败了38.60% 的用户
通过测试用例：187 / 187

```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        # 真的写的很挫
        # 用0分割数组，然后再子数组找到乘积最大的
        # 再在所有子数组中找最大的
        if nums == [0]:
            return 0
        def subfunc(nums_):

            res1 = 1
            _list =[]
            res = []
            res2 = False
            for i in nums_:
                if i > 0:
                    if res1 > 0:
                        res.append(res1*i)
                    elif res1 < 0:
                        res.append(res2*i)
                    if res2:
                        res2 *= i
                    res1 *= i
                elif i < 0:
                    if not res2:
                        res2 = 1
                        res1 *= i
                        if not res:
                            res.append(i)
                        continue
                    if res1 > 0:
                        res.append(res2*i)
                    elif res1 < 0:
                        res.append(res1*i)
                    res2 *= i
                    res1 *= i
            return max(res)
        nums_ = []
        temp = []
        flag = False
        for i in nums:
            if i != 0:
                temp.append(i)
            else:
                flag = True
                if temp:
                    nums_.append(temp)
                temp = []
        if temp:
            nums_.append(temp)
        res = []
        for i in nums_:
            res.append(subfunc(i))
        if flag:
            return max(max(res), 0)
        else:
            return max(res)

```
**Tag: 栈、数组、单调栈**

# 打家劫舍

Link => [打家劫舍](https://leetcode-cn.com/problems/house-robber/)

## 题目
你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响你偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。

给定一个代表每个房屋存放金额的非负整数数组，计算你 不触动警报装置的情况下 ，一夜之内能够偷窃到的最高金额。

**示例1**
>输入：[1,2,3,1]<br />
>输出：4<br />
>解释：偷窃 1 号房屋 (金额 = 1) ，然后偷窃 3 号房屋 (金额 = 3)。<br />
>偷窃到的最高金额 = 1 + 3 = 4 <br />

**示例2**
>输入：[2,7,9,3,1]<br />
>输出：12<br />
>解释：偷窃 1 号房屋 (金额 = 2), 偷窃 3 号房屋 (金额 = 9)，接着偷窃 5 号房屋 (金额 = 1)。<br />
>偷窃到的最高金额 = 2 + 9 + 1 = 12 。<br />

执行结果：
通过
显示详情

添加备注
执行用时：32 ms, 在所有 Python3 提交中击败了64.96% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了5.00% 的用户
通过测试用例：68 / 68

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        # 想着用动态规划了，但是貌似存了太多没有用的量
        # dp[i]表示偷当前屋子情况下的最大偷钱数
        max_list = []
        dp = [0 for i in nums]
        for i in range(len(nums)):
            if i == 0:
                dp[0] = nums[0]
                max_list.append(dp[0])
            elif i == 1:
                dp[1] = nums[1]
                max_list.append(max(max_list[-1], dp[1]))
            else:
                dp[i] = nums[i] + max_list[i - 2]
                max_list.append(max(max_list[-1], dp[i]))


        return max_list[-1]
```
改进：
省一点内存
执行结果：
通过
显示详情

添加备注
执行用时：32 ms, 在所有 Python3 提交中击败了64.96% 的用户
内存消耗：14.9 MB, 在所有 Python3 提交中击败了76.53% 的用户
通过测试用例：68 / 68

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        # 其实不用存每一个，存下当前最大的就行
        _max = 0 # 和上面写的max_list同理，本来是求出本次的dp，再比较dp是不是当前最大的，合为一步，存一个_max
        _max_1 = 0 # 存一下_max的前一个数，为了传递到_max_2
        _max_2 = 0
        for i in range(len(nums)):
            _max_2 = _max_1
            _max_1 = _max
            _max = max(_max, nums[i] + _max_2)

        return _max
```
**Tag: 数组、动态规划**

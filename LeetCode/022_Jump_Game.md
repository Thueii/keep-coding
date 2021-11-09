# 跳跃游戏

Link => [跳跃游戏](https://leetcode-cn.com/problems/jump-game/)
给定一个非负整数数组 nums ，你最初位于数组的 第一个下标 。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个下标。

>输入：nums = [2,3,1,1,4]<br />
>输出：true<br />
>解释：可以先跳 1 步，从下标 0 到达下标 1, 然后再从下标 1 跳 3 步到达最后一个下标。<br />

>输入：nums = [3,2,1,0,4]<br />
>输出：false<br />
>解释：无论怎样，总会到达下标为 3 的位置。但该下标的最大跳跃长度是 0 ， 所以永远不可能到达最后一个下标.<br />

执行结果：
通过
显示详情

添加备注
执行用时：72 ms, 在所有 Python3 提交中击败了89.70% 的用户
内存消耗：15.3 MB, 在所有 Python3 提交中击败了67.89% 的用户
通过测试用例：166 / 166


```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        # 维护一个最远距离，即当前点上能到达的最远距离
        # 同时要理解，当有一个最远距离则前面所谓位置的点都可以到达
        max_ = 0
        for i in range(len(nums)):
            if i <= max_ and i + nums[i] > max_:
                max_ = i + nums[i]
            elif i > max_:
                break
        return max_ >= len(nums) - 1
```
**Tag: 贪心、数组、动态规划**

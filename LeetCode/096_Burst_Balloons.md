# 戳气球

Link => [戳气球](https://leetcode-cn.com/problems/burst-balloons/)

## 题目

    有 n 个气球，编号为0 到 n - 1，每个气球上都标有一个数字，这些数字存在数组 nums 中。

    现在要求你戳破所有的气球。戳破第 i 个气球，你可以获得 nums[i - 1] * nums[i] * nums[i + 1] 枚硬币。 这里的 i - 1 和 i + 1 代表和 i 相邻的两个气球的序号。如果 i - 1或 i + 1 超出了数组的边界，那么就当它是一个数字为 1 的气球。

    求所能获得硬币的最大数量。

**示例1**

    输入：nums = [3,1,5,8]
    输出：167
    解释：
    nums = [3,1,5,8] --> [3,5,8] --> [3,8] --> [8] --> []
    coins =  3*1*5    +   3*5*8   +  1*3*8  + 1*8*1 = 167

**示例2**
    输入：nums = [1,5]
    输出：10

**执行结果：通过 显示详情**
全排列算的，不出意外

- 超时

```python
class Solution:
    def maxCoins(self, nums: List[int]) -> int:
        res = 0
        def dfs(cur_list, cur_sum):
            nonlocal res
            if not cur_list:
                res = max(res, cur_sum)
                return
            max_len = len(cur_list)
            for i in range(len(cur_list)):
                if max_len == 1:
                    tmp = cur_list.pop()
                    dfs(cur_list, cur_sum+tmp)
                    cur_list.append(tmp)
                elif i == 0:
                    tmp = cur_list[0]
                    tmp_sum = tmp*cur_list[1]
                    cur_list.pop(0)
                    dfs(cur_list, cur_sum+tmp_sum)
                    cur_list.insert(0, tmp)
                elif i == max_len -1:
                    tmp = cur_list[-1]
                    tmp_sum = tmp*cur_list[-2]
                    cur_list.pop()
                    dfs(cur_list, cur_sum+tmp_sum)
                    cur_list.append(tmp)
                else:
                    tmp = cur_list[i]
                    tmp_sum = tmp*cur_list[i-1]*cur_list[i+1]
                    cur_list.pop(i)
                    dfs(cur_list, cur_sum+tmp_sum)
                    cur_list.insert(i, tmp)
        dfs(nums, 0)
        return res
```
**改进**
这题一看就要用动态规划，但是不知道怎么规划，一直想着从哪个开头，其实不然，应该从哪个结束开始想
这样能把分析分为两部分，且连续，但是自己肯定想不出来= =，看了一晚上题解加上早上，才看到一个，终于懂了
其实拿回溯的想法更容易懂，我放最下面po上吧

- 执行用时：5640 ms, 在所有 Python3 提交中击败了71.18% 的用户
内存消耗：20.3 MB, 在所有 Python3 提交中击败了94.71% 的用户
通过测试用例：71 / 71

```python
class Solution:
    def maxCoins(self, nums: List[int]) -> int:
        # 打一下log才知道小这个做小区间再到大区间是什么意思
        nums = [1] + nums + [1]
        memo = [[0]*len(nums) for i in range(len(nums))]

        def cal_k(i, j):
            tmp = 0
            for k in range(i+1, j):
                left = memo[i][k]
                right = memo[k][j]
                tmp = max(tmp, left+right+nums[i]*nums[j]*nums[k])
            memo[i][j] = tmp

        for n in range(2, len(nums)):
            for i in range(0, len(nums)-n):
                cal_k(i,i+n)

        return memo[0][len(nums)-1]

```
看一下log，平移小区间，把所有的情况都搞定以后在大区间的时候就可以利用小空间做好的数据，
我感觉这题最难的是理解这个小区间到大区间，想这个循环想了好久，一直看不懂，打了log终于懂了
```
0 2
取:  0 1
取:  1 2
1 3
取:  1 2
取:  2 3
2 4
取:  2 3
取:  3 4
3 5
取:  3 4
取:  4 5
0 3
取:  0 1
取:  1 3
取:  0 2
取:  2 3
1 4
取:  1 2
取:  2 4
取:  1 3
取:  3 4
2 5
取:  2 3
取:  3 5
取:  2 4
取:  4 5
0 4
取:  0 1
取:  1 4
取:  0 2
取:  2 4
取:  0 3
取:  3 4
1 5
取:  1 2
取:  2 5
取:  1 3
取:  3 5
取:  1 4
取:  4 5
0 5
取:  0 1
取:  1 5
取:  0 2
取:  2 5
取:  0 3
取:  3 5
取:  0 4
取:  4 5
```
**回溯**
再放一个回溯的思路，比较好想，但是超级慢
```python
class Solution:
    def maxCoins(self, nums: List[int]):
        if not nums:
            return 0
        
        def getMaxCoins(nums, i, j, memo):
            if i == j - 1:
                return 0
            if memo[i][j] > 0:
                return memo[i][j]
            
            temp = 0
            for k in range(i + 1, j):
                left = getMaxCoins(nums, i, k, memo)
                right = getMaxCoins(nums, k, j, memo)
                temp = max(temp, left + right + nums[i] * nums[k] * nums[j])

            memo[i][j] = temp
            return temp

        nums = [1, *nums, 1]
        memo = [[0 for i in nums] for n in nums]

        return getMaxCoins(nums, 0, len(nums) - 1, memo)
```
**Tag: 数组、动态规划**

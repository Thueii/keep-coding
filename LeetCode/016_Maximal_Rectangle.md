# 最大矩形

Link => [最大矩形](https://leetcode-cn.com/problems/maximal-rectangle/)

给定一个仅包含 0 和 1 、大小为 rows x cols 的二维二进制矩阵，找出只包含 1 的最大矩形，并返回其面积。

>输入：matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]<br />
>输出：6<br />

执行结果：
通过
显示详情

添加备注
执行用时：300 ms, 在所有 Python3 提交中击败了12.47% 的用户
内存消耗：21.1 MB, 在所有 Python3 提交中击败了5.07% 的用户
通过测试用例：71 / 71

ps：写的太辣鸡了

```python
class Solution:
    def maximalRectangle(self, matrix: List[List[str]]) -> int:
        if matrix == []:
            return 0
        height = len(matrix)
        width = len(matrix[0])
        dp = [[[0, 0] for i in range(width)] for j in range(height)]
        max_s = 0

        for j in range(height):
            for i in range(width):
                if matrix[j][i] == "0":
                    continue
                else:
                    if j == 0:
                        if i == 0:
                            dp[j][i] = [1, 1]
                            max_s = 1
                        else:
                            dp[j][i] = [dp[j][i-1][0] + 1, 1]
                            max_s = max(max_s, dp[j][i][0])
                    else:
                        if i == 0:
                            dp[j][i] = [1, dp[j-1][i][1] + 1]
                            max_s = max(max_s, dp[j][i][1])
                        else:
                            # 看左边连续1
                            dp[j][i][0] = dp[j][i-1][0] + 1
                            # 看右边连续1
                            dp[j][i][1] = dp[j-1][i][1] + 1

                            # 计算面积
                            # 定左边界
                            
                            min_left = float(inf)
                            count1 = 0
                            while True:
                                if j - count1 < 0 or dp[j-count1][i][0] == 0 or dp[j-count1][i][0] == 1:
                                    break
                                min_left = min(min_left, dp[j-count1][i][0])
                                count1 += 1
                            max_s_shuzhede = min_left * (j-(j-(count1)))

                            # 定定上边界
                            min_up = float(inf)
                            count2 = 0
                            while True:
                                if i - count2 < 0 or dp[j][i-count2][1] == 0 or dp[j][i-count2][1] == 1:
                                    break
                                min_up = min(min_up, dp[j][i-count2][1])
                                count2 += 1
                            max_s_hengzhede = min_up * (i-(i-(count2)))
                            
                            max_s = max(max_s, max_s_hengzhede, max_s_shuzhede, dp[j][i][0], dp[j][i][1])

        return max_s
```
改进：
暴力法

通过
显示详情

添加备注
执行用时：256 ms, 在所有 Python3 提交中击败了15.12% 的用户
内存消耗：20.2 MB, 在所有 Python3 提交中击败了85.24% 的用户
通过测试用例：71 / 71

```python
class Solution:
    def maximalRectangle(self, matrix: List[List[str]]) -> int:
        if matrix == []:
            return 0
        height = len(matrix)
        width = len(matrix[0])
        dp = [[0 for i in range(width)] for j in range(height)]
        max_s = 0
        for j in range(height):
            for i in range(width):
                if matrix[j][i] == "0":
                    dp[j][i] = 0
                else:
                    if i == 0:
                        dp[j][i] = 1
                    else:
                        dp[j][i] = dp[j][i-1] + 1

                    # 计算面积
                    max_s = max(dp[j][i], max_s)
                    count = 0 
                    chang = dp[j][i] 
                    while True:
                        if j - count < 0 or dp[j-count][i] == 0:
                            break
                        if dp[j-count][i] > chang:
                            max_s = max(max_s, chang * (j-(j-count)+1))
                        else:
                            chang = dp[j-count][i]
                            max_s = max(max_s, chang * (j-(j-count)+1))
                        count += 1

        return max_s
```
改进：
单调栈
执行结果：
通过
显示详情

添加备注
执行用时：80 ms, 在所有 Python3 提交中击败了63.54% 的用户
内存消耗：20.6 MB, 在所有 Python3 提交中击败了5.07% 的用户
通过测试用例：71 / 71
```python
class Solution:
    def maximalRectangle(self, matrix: List[List[str]]) -> int:
        if matrix == []:
            return 0
        height = len(matrix)
        width = len(matrix[0])
        dp = [[0 for i in range(width)] for j in range(height)]
        max_s = 0
        for j in range(height):
            for i in range(width):
                if matrix[j][i] == "0":
                    dp[j][i] = 0
                else:
                    if i == 0:
                        dp[j][i] = 1
                    else:
                        dp[j][i] = dp[j][i-1] + 1

        for j in range(width):
            stack = []

            for index in range(height):
                if index == 0:
                    stack.append(index)
                else:
                    while stack and dp[stack[-1]][j] > dp[index][j]:
                        now = dp[stack.pop()][j]
                        if stack:
                            max_s = max(max_s, (index-stack[-1]-1)*now)
                        else:
                            max_s = max(max_s, (index-(-1)-1)*now)

                    stack.append(index)

            while len(stack) > 1:
                now = stack.pop()
                max_s = max(max_s, ((height)-stack[-1]-1)*dp[now][j])
            if len(stack) == 1:
                now = stack.pop()
                max_s = max(max_s, (((height)-(-1)-1)*dp[now][j]))

        return max_s
```
**Tag: 栈、数组、动态规划、矩阵、单调栈**

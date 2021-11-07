# 每日温度

Link => [每日温度](https://leetcode-cn.com/problems/daily-temperatures/)
请根据每日 气温 列表 temperatures ，请计算在每一天需要等几天才会有更高的温度。如果气温在这之后都不会升高，请在该位置用 0 来代替。

>输入：temperatures = [73,74,75,71,69,72,76,73]<br />
>输出：[1,1,4,2,1,1,0,0]<br />

>输入：temperatures = [30,40,50,60]<br />
>输出：[1,1,1,0]<br />

执行结果：
通过
显示详情

添加备注
执行用时：192 ms, 在所有 Python3 提交中击败了62.25% 的用户
内存消耗：21 MB, 在所有 Python3 提交中击败了11.60% 的用户
通过测试用例：47 / 47

```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        stack = []
        res = [0 for i in temperatures]
        for i in range(len(temperatures)):
            if not stack:
                stack.append(i)
            else:
                if temperatures[i] <= temperatures[stack[-1]]:
                    stack.append(i)
                else:
                    while stack and temperatures[i] > temperatures[stack[-1]]:
                        now_index = stack.pop()
                        res[now_index] = i - now_index
                    stack.append(i)
        for i in stack:
            res[i] = 0
        return res
```
**Tag: 栈、数组、单调栈**

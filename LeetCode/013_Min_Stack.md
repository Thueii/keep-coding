# 最小栈

Link => [最小栈](https://leetcode-cn.com/problems/min-stack/)

设计一个支持 push ，pop ，top 操作，并能在常数时间内检索到最小元素的栈。

    push(x) —— 将元素 x 推入栈中。
    pop() —— 删除栈顶的元素。
    top() —— 获取栈顶元素。
    getMin() —— 检索栈中的最小元素。

>输入：["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]<br />
>输出：[null,null,null,null,-3,null,0,-2]<br />

执行结果：
通过
显示详情

添加备注
执行用时：56 ms, 在所有 Python3 提交中击败了64.33% 的用户
内存消耗：18.3 MB, 在所有 Python3 提交中击败了11.55% 的用户
通过测试用例：31 / 31

```python
class MinStack:

    def __init__(self):
        self.item = []
        self.min_stack = []

    def push(self, val: int) -> None:
        self.item.append(val)
        if self.min_stack == []:
            self.min_stack.append(val)
        else:
            self.min_stack.append(min(self.min_stack[-1], val))
    def pop(self) -> None:
        self.item.pop()
        self.min_stack.pop()

    def top(self) -> int:
        return self.item[-1]

    def getMin(self) -> int:
        return self.min_stack[-1]


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(val)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```
改进：
执行结果：
通过
显示详情

添加备注
执行用时：48 ms, 在所有 Python3 提交中击败了92.00% 的用户
内存消耗：18 MB, 在所有 Python3 提交中击败了48.26% 的用户
通过测试用例：31 / 31

```python
class MinStack:

    def __init__(self):
        self.item = []
        self.min_stack = []

    def push(self, val: int) -> None:
        self.item.append(val)
        if not self.min_stack or val <= self.min_stack[-1]:
            self.min_stack.append(val)

    def pop(self) -> None:
        pop_num = self.item.pop()
        if pop_num == self.min_stack[-1]:
            self.min_stack.pop()

    def top(self) -> int:
        return self.item[-1]

    def getMin(self) -> int:
        return self.min_stack[-1]


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(val)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```
**Tag: 栈、设计**

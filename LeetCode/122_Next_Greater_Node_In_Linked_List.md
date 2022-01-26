# 链表中的下一个更大节点

Link => [链表中的下一个更大节点](https://leetcode-cn.com/problems/next-greater-node-in-linked-list/)

## 题目

    给出一个以头节点 head 作为第一个节点的链表。链表中的节点分别编号为：node_1, node_2, node_3, ... 。

    每个节点都可能有下一个更大值（next larger value）：对于 node_i，如果其 next_larger(node_i) 是 node_j.val，那么就有 j > i 且  node_j.val > node_i.val，而 j 是可能的选项中最小的那个。如果不存在这样的 j，那么下一个更大值为 0 。

    返回整数答案数组 answer，其中 answer[i] = next_larger(node_{i+1}) 。

    注意：在下面的示例中，诸如 [2,1,5] 这样的输入（不是输出）是链表的序列化表示，其头节点的值为 2，第二个节点值为 1，第三个节点值为 5 。

**示例1**

    输入：[2,1,5]
    输出：[5,5,0]

**示例2**

    输入：[2,7,4,3,5]
    输出：[7,0,5,5,0]


**执行结果：通过 显示详情**
常规做法，只解决了部分问题

- 执行用时：220 ms, 在所有 Python3 提交中击败了17.67% 的用户
内存消耗：19.2 MB, 在所有 Python3 提交中击败了35.35% 的用户
通过测试用例：76 / 76

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def nextLargerNodes(self, head: Optional[ListNode]) -> List[int]:
        if not head:
            return head
        stack = []
        p = head
        while p:
            stack.append(p.val)
            p = p.next
        reverse_list = stack[::-1]
        max_num=-inf
        for i in range(len(reverse_list)):
            max_num = max(max_num, reverse_list[i])
            reverse_list[i] = max_num
        stack2 = reverse_list[::-1]
        for i in range(len(stack)):
            if stack[i] >= stack2[i]:
                stack[i] = 0
            else:
                for j in range(i, len(stack)):
                    if stack[j] > stack[i]:
                        stack[i] = stack[j]
                        break
        return stack
```
**改进**
单调栈，简单
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def nextLargerNodes(self, head: Optional[ListNode]) -> List[int]:
        if not head:
            return head
        alist = []
        p = head
        while p:
            alist.append(p.val)
            p = p.next
        alist = alist[::-1]
        stack = []
        for i in range(len(alist)):
            if not stack:
                stack.append(alist[i])
                alist[i] = 0
            else:
                while stack and stack[-1] <= alist[i]:
                    stack.pop()
                stack.append(alist[i])
                if len(stack) == 1:
                    alist[i] = 0
                else:
                    alist[i] = stack[-2]
        return alist[::-1]
```
**Tag: 栈、数组、链表、单调栈**

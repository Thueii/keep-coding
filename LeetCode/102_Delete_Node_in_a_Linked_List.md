#  删除链表中的节点

Link => [删除链表中的节点](https://leetcode-cn.com/problems/delete-node-in-a-linked-list/)

## 题目

    请编写一个函数，用于 删除单链表中某个特定节点 。在设计函数时需要注意，你无法访问链表的头节点 head ，只能直接访问 要被删除的节点 。

    题目数据保证需要删除的节点 不是末尾节点 。


**示例1**

    输入：head = [4,5,1,9], node = 5
    输出：[4,1,9]
    解释：指定链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9

**示例2**

    输入：head = [4,5,1,9], node = 1
    输出：[4,5,9]
    解释：指定链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9


**执行结果：通过 显示详情**
入门级别

- 执行用时：40 ms, 在所有 Python3 提交中击败了59.77% 的用户
内存消耗：15.4 MB, 在所有 Python3 提交中击败了73.79% 的用户
通过测试用例：41 / 41

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def deleteNode(self, node):
        """
        :type node: ListNode
        :rtype: void Do not return anything, modify node in-place instead.
        """
        node.val = node.next.val
        node.next = node.next.next
```

**Tag: 链表**

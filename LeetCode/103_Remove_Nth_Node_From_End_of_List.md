#  删除链表的倒数第 N 个结点

Link => [删除链表的倒数第 N 个结点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)

## 题目

    给你一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。


**示例1**

    输入：head = [1,2,3,4,5], n = 2
    输出：[1,2,3,5]

**示例2**

    输入：head = [1], n = 1
    输出：[]


**执行结果：通过 显示详情**
双指针

- 执行用时：36 ms, 在所有 Python3 提交中击败了48.69% 的用户
内存消耗：15 MB, 在所有 Python3 提交中击败了42.69% 的用户
通过测试用例：208 / 208

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        fast = head
        slow = head
        pre = ListNode(-1)
        a = pre
        for i in range(n-1):
            fast = fast.next
        while fast.next != None:
            pre.next = slow
            pre = pre.next
            slow = slow.next
            fast = fast.next
        pre.next = slow.next
        slow = slow.next
        return a.next
```

**Tag: 链表**

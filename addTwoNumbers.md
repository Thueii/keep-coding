# 两数相加

Link => [两数相加](https://leetcode-cn.com/problems/add-two-numbers/)

**题目：给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。请你将两个数相加，并以相同形式返回一个表示和的链表。你可以假设除了数字 0 之外，这两个数都不会以 0 开头。**

> 示例 1：<br />
> 输入：l1 = [2,4,3], l2 = [5,6,4]<br />
> 输出：[7,0,8]<br />
> 解释：342 + 465 = 807.<br />
> 
> 示例 2：<br />
> 输入：l1 = [0], l2 = [0]<br />
> 输出：[0]<br />
> 
> 示例 3：<br />
> 输入：l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]<br />
> 输出：[8,9,9,9,0,0,0,1]<br />

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        start = ListNode()
        p = start
        while l1 or l2 :
            if l1 is None:
                l1 = ListNode(0)
            if l2 is None:
                l2 = ListNode(0)
            div = (l1.val + l2.val + start.val) // 10
            quo = (l1.val + l2.val + start.val) % 10
            start.val = quo
            l1 = l1.next
            l2 = l2.next
            if div == 1 or l1 or l2:
                temp = ListNode()
                temp.val = div
                start.next = temp
                start = temp
            
        return p
```

**Tag: 递归、链表、数学**

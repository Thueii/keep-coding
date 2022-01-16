#  两数相加

Link => [两数相加](https://leetcode-cn.com/problems/add-two-numbers/)

## 题目

    给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。

    请你将两个数相加，并以相同形式返回一个表示和的链表。

    你可以假设除了数字 0 之外，这两个数都不会以 0 开头。


**示例1**

    输入：l1 = [2,4,3], l2 = [5,6,4]
    输出：[7,0,8]
    解释：342 + 465 = 807.

**示例2**

    输入：l1 = [0], l2 = [0]
    输出：[0]



**执行结果：通过 显示详情**
注意一个div的传递

- 执行用时：64 ms, 在所有 Python3 提交中击败了19.76% 的用户
内存消耗：14.8 MB, 在所有 Python3 提交中击败了98.81% 的用户
通过测试用例：1568 / 1568

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        s = ListNode()
        p = s
        while l1 or l2:
            if not l1:
                l1 = ListNode(0)
            if not l2:
                l2 = ListNode(0)
            div = (l1.val+l2.val+p.val) // 10
            quo = (l1.val+l2.val+p.val) % 10
            p.val = quo
            l1 = l1.next
            l2 = l2.next
            if div == 1 or l1 or l2:
                tmp = ListNode(div)
                p.next = tmp
                p = tmp
            
        return s
```

**Tag: 链表、递归、数学**

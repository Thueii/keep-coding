#  反转链表 II

Link => [反转链表 II](https://leetcode-cn.com/problems/reverse-linked-list-ii/)

## 题目

    给你单链表的头指针 head 和两个整数 left 和 right ，其中 left <= right 。请你反转从位置 left 到位置 right 的链表节点，返回 反转后的链表 。

**示例1**

    输入：head = [1,2,3,4,5], left = 2, right = 4
    输出：[1,4,3,2,5]

**示例2**

    输入：head = [5], left = 1, right = 1
    输出：[5]


**执行结果：通过 显示详情**
定位两个位置，然后造中间的next

- 执行用时：36 ms, 在所有 Python3 提交中击败了39.25% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了49.90% 的用户
通过测试用例：44 / 44

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseBetween(self, head: ListNode, left: int, right: int) -> ListNode:
        a = ListNode(-1)
        a.next = head
        pre = None
        cur = a
        for i in range(left):
            pre1 = cur
            cur = cur.next
        last = cur
        for j in range(left-1,right):
            temp = cur.next
            cur.next = pre
            pre = cur
            cur = temp
        pre1.next = pre
        last.next = cur
        return a.next
```

**Tag: 链表、双指针**

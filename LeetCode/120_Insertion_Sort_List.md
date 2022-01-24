# 对链表进行插入排序

Link => [对链表进行插入排序](https://leetcode-cn.com/problems/partition-list/)

## 题目

    对链表进行插入排序。


    插入排序的动画演示如上。从第一个元素开始，该链表可以被认为已经部分排序（用黑色表示）。
    每次迭代时，从输入数据中移除一个元素（用红色表示），并原地将其插入到已排好序的链表中。

**示例1**

    输入: 4->2->1->3
    输出: 1->2->3->4

**示例2**

    输入: -1->5->3->4->0
    输出: -1->0->3->4->5


**执行结果：通过 显示详情**
感觉不是很妙

- 执行用时：148 ms, 在所有 Python3 提交中击败了69.38% 的用户
内存消耗：17.1 MB, 在所有 Python3 提交中击败了5.45% 的用户
通过测试用例：19 / 19

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def insertionSortList(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head
        cur, nxt = head, head.next
        dummy = ListNode(float('-inf'))
        dummy.next = head # 返回用
        while nxt:
            if nxt.val >= cur.val:
                cur = cur.next
                nxt = nxt.next
            else:
                nxt_next = nxt.next 
                pre1, pre2 = dummy, dummy.next
                while pre2 and pre2.val < nxt.val:
                    pre1 = pre2
                    pre2 = pre2.next
                nxt.next = pre1.next
                pre1.next = nxt
                cur.next = nxt_next
                nxt = cur.next
        return dummy.next
```

**Tag: 链表、排序**

#  移除链表元素

Link => [移除链表元素](https://leetcode-cn.com/problems/remove-linked-list-elements/)

## 题目

    给你一个链表的头节点 head 和一个整数 val ，请你删除链表中所有满足 Node.val == val 的节点，并返回 新的头节点 。 


**示例1**

    输入：head = [1,2,6,3,4,5,6], val = 6
    输出：[1,2,3,4,5]

**示例2**

    输入：head = [], val = 1
    输出：[]


**执行结果：通过 显示详情**
没啥好说的

- 执行用时：64 ms, 在所有 Python3 提交中击败了32.98% 的用户
内存消耗：17.9 MB, 在所有 Python3 提交中击败了63.86% 的用户
通过测试用例：66 / 66

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeElements(self, head: ListNode, val: int) -> ListNode:
        dummy = ListNode(-1)
        dummy.next = head
        cur = dummy
        while cur:
            if cur.next and cur.next.val == val:
                cur.next = cur.next.next
            else:
                cur = cur.next
        return dummy.next
```

**Tag: 链表**

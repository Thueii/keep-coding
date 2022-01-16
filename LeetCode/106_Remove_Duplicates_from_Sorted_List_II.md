#  删除排序链表中的重复元素 II

Link => [删除排序链表中的重复元素 II](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/)

## 题目

   存在一个按升序排列的链表，给你这个链表的头节点 head ，请你删除链表中所有存在数字重复情况的节点，只保留原始链表中 没有重复出现 的数字。

    返回同样按升序排列的结果链表。



**示例1**

    输入：head = [1,2,3,3,4,4,5]
    输出：[1,2,5]

**示例2**

    输入：head = [1,1,1,2,3]
    输出：[2,3]


**执行结果：通过 显示详情**
或者双指针

- 执行用时：44 ms, 在所有 Python3 提交中击败了31.03% 的用户
内存消耗：15.2 MB, 在所有 Python3 提交中击败了5.23% 的用户
通过测试用例：166 / 166

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        cur = head
        dup = set()
        while cur and cur.next:
            if cur.val == cur.next.val:
                dup.add(cur.val)
            cur = cur.next
        dummy = ListNode(-1)
        dummy.next = head
        cur = dummy
        while cur:
            if cur.next and cur.next.val in dup:
                cur.next = cur.next.next
            else:
                cur = cur.next
        return dummy.next
```

**Tag: 链表、双指针**

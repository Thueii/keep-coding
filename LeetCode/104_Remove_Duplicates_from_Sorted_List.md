#  删除排序链表中的重复元素

Link => [删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)

## 题目

    存在一个按升序排列的链表，给你这个链表的头节点 head ，请你删除所有重复的元素，使每个元素 只出现一次 。

    返回同样按升序排列的结果链表。


**示例1**

    输入：head = [1,1,2]
    输出：[1,2]

**示例2**

    输入：head = [1,1,2,3,3]
    输出：[1,2,3]


**执行结果：通过 显示详情**
双指针

- 执行用时：36 ms, 在所有 Python3 提交中击败了82.22% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了24.64% 的用户
通过测试用例：166 / 166

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        pre = head
        while pre:
            if pre.next and pre.next.val == pre.val:
                pre.next = pre.next.next
            else:
                pre = pre.next
        return head
```

**Tag: 链表**

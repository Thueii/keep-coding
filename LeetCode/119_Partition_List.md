# 分隔链表

Link => [分隔链表](https://leetcode-cn.com/problems/partition-list/)

## 题目

    给你一个链表的头节点 head 和一个特定值 x ，请你对链表进行分隔，使得所有 小于 x 的节点都出现在 大于或等于 x 的节点之前。

    你应当 保留 两个分区中每个节点的初始相对位置。

**示例1**

    输入：head = [1,4,3,2,5,2], x = 3
    输出：[1,2,2,4,3,5]

**示例2**

    输入：head = [2,1], x = 2
    输出：[1,2]


**执行结果：通过 显示详情**
我牛逼

- 执行用时：28 ms, 在所有 Python3 提交中击败了94.78% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了5.08% 的用户
通过测试用例：168 / 168

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def partition(self, head: ListNode, x: int) -> ListNode:
        cur = head
        les_pre = ListNode(-1)
        les_head = les_pre
        great_pre = ListNode(-1)
        great_head = great_pre
        while cur:
            if cur.val < x:
                les_pre.next = cur
                les_pre = cur
            else:
                great_pre.next = cur
                great_pre = cur
            cur = cur.next
        great_pre.next = None
        les_pre.next = great_head.next
        return les_head.next
```

**Tag: 链表、双指针**

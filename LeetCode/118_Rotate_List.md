# 旋转链表

Link => [旋转链表](https://leetcode-cn.com/problems/rotate-list/)

## 题目

    给你一个链表的头节点 head ，旋转链表，将链表每个节点向右移动 k 个位置。

**示例1**

    输入：head = [1,2,3,4,5], k = 2
    输出：[4,5,1,2,3]

**示例2**

    输入：head = [0,1,2], k = 4
    输出：[2,0,1]

**执行结果：通过 显示详情**
快慢指针

- 执行用时：28 ms, 在所有 Python3 提交中击败了97.87% 的用户
内存消耗：15 MB, 在所有 Python3 提交中击败了16.93% 的用户
通过测试用例：231 / 231

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def rotateRight(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:  
        if not head or not head.next:
            return head
        count = 0
        cur = head
        while cur:
            count+=1
            cur = cur.next 
        k %= count
        if k == 0:
            return head
        slow, fast = head, head
        for _ in range(k):
            fast = fast.next
        while fast and fast.next:
            fast = fast.next
            slow = slow.next
        res_start = slow.next
        slow.next = None
        fast.next = head
        return res_start
```

**Tag: 链表、双指针**

# 重排链表

Link => [重排链表](https://leetcode-cn.com/problems/reorder-list/)

## 题目

    给定一个单链表 L 的头节点 head ，单链表 L 表示为：
    L0 → L1 → … → Ln - 1 → Ln

    请将其重新排列后变为：

    L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
    不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

**示例1**

    输入：head = [1,2,3,4]
    输出：[1,4,2,3]

**示例2**

    输入：head = [1,2,3,4,5]
    输出：[1,5,2,4,3]

**执行结果：通过 显示详情**
注意中间的要next= None

- 执行用时：56 ms, 在所有 Python3 提交中击败了98.92% 的用户
内存消耗：23.2 MB, 在所有 Python3 提交中击败了40.93% 的用户
通过测试用例：12 / 12

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reorderList(self, head: ListNode) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        root = head
        adict = {}
        idx = 0
        while head:
            adict[idx] = head
            head = head.next
            idx += 1
        l, r = 0, idx - 1
        while l < r:
            adict[l].next = adict[r]
            adict[r].next = adict[l+1]
            l += 1
            r -= 1
        adict[idx//2].next = None
```

**Tag: 栈、递归、链表、双指针**

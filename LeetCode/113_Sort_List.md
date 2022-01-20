# 排序链表

Link => [排序链表](https://leetcode-cn.com/problems/sort-list/)

## 题目

    给你链表的头结点 head ，请将其按 升序 排列并返回 排序后的链表 。


**示例1**

    输入：head = [4,2,1,3]
    输出：[1,2,3,4]

**示例2**

    输入：head = [-1,5,3,4,0]
    输出：[-1,0,3,4,5]

**执行结果：通过 显示详情**
常规做法

- 执行用时：164 ms, 在所有 Python3 提交中击败了90.72% 的用户
内存消耗：38.2 MB, 在所有 Python3 提交中击败了5.62% 的用户
通过测试用例：28 / 28

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def sortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        alist = []
        while head:
            alist.append(head.val)
            head = head.next
        alist.sort()
        print(alist)
        dummy = ListNode(-1)
        p = dummy
        for num in alist:
            tmp = ListNode(num)
            dummy.next = tmp
            dummy = tmp

        return p.next
```

**Tag: 链表、双指针、分治、排序、归并排序**

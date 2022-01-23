# K 个一组翻转链表

Link => [K 个一组翻转链表](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)

## 题目

    给你一个链表，每 k 个节点一组进行翻转，请你返回翻转后的链表。

    k 是一个正整数，它的值小于或等于链表的长度。

    如果节点总数不是 k 的整数倍，那么请将最后剩余的节点保持原有顺序。

    进阶：

        你可以设计一个只使用常数额外空间的算法来解决此问题吗？
        你不能只是单纯的改变节点内部的值，而是需要实际进行节点交换。

**示例1**

    输入：head = [1,2,3,4,5], k = 2
    输出：[2,1,4,3,5]


**执行结果：通过 显示详情**
根据题意做的，没有什么特别的
- 执行用时：40 ms, 在所有 Python3 提交中击败了80.74% 的用户
内存消耗：15.7 MB, 在所有 Python3 提交中击败了39.21% 的用户
通过测试用例：62 / 62

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        def reverse_sub_group(sub_list):
            prev = None
            while sub_list:
                nex = sub_list.next
                sub_list.next = prev
                prev = sub_list
                sub_list = nex
            return prev

        dummy = ListNode(-1)
        pre_node = dummy
        cur = head
        while cur:
            count = 1
            start = cur
            while count < k and cur.next:
                cur = cur.next
                count += 1
            if count == k:
                if cur:
                    nex = cur.next
                    cur.next = None
                    cur = nex
                pre_node.next = reverse_sub_group(start)
                start.next = cur
                pre_node = start
            else:
                cur = cur.next
        return dummy.next
```

**Tag: 链表、双指针、分治、排序、归并排序**

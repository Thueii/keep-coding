# 合并两个有序链表

Link => [合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)

## 题目
将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。

**示例1**
>输入：l1 = [1,2,4], l2 = [1,3,4]<br />
>输出：[1,1,2,3,4,4]<br />

**示例2**
>输入：l1 = [], l2 = []<br />
>输出：[]<br />

**执行结果：通过 显示详情**
不确定对不对，看起来打败的百分比来说不太对= =。。。。

- 执行用时：40 ms, 在所有 Python3 提交中击败了33.69% 的用户
内存消耗：14.9 MB, 在所有 Python3 提交中击败了81.14% 的用户
通过测试用例：208 / 208

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        res_head = ListNode()
        p = res_head
        while list1 or list2:
            if list1 and list2:
                if list1.val < list2.val:
                    p.next = list1
                    list1 = list1.next
                else:
                    p.next = list2
                    list2 = list2.next
            elif list1:
                p.next = list1
                list1 = list1.next
            else:
                p.next = list2
                list2 = list2.next
            p = p.next
        return res_head.next
```
**改进**
改进了一下自己的，可以提前跳出循环

- 执行用时：32 ms, 在所有 Python3 提交中击败了86.48% 的用户
内存消耗：14.9 MB, 在所有 Python3 提交中击败了79.40% 的用户
通过测试用例：208 / 208
```python
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        res_head = p = ListNode() # 可以连等式
        while list1 and list2:
            if list1.val < list2.val:
                p.next = list1
                list1 = list1.next
            else:
                p.next = list2
                list2 = list2.next
            p = p.next
        p.next = list1 if list1 else list2
        return res_head.next
```
**改进**
用递归，很巧妙，每次做的是把两个链表中小的那个作为list1，然后找list1.next，再利用递归

- 执行用时：36 ms, 在所有 Python3 提交中击败了63.63% 的用户
内存消耗：14.9 MB, 在所有 Python3 提交中击败了68.56% 的用户
通过测试用例：208 / 208

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        if list1 and list2:
            if list1.val > list2.val: list1, list2 = list2, list1
            list1.next = self.mergeTwoLists(list1.next, list2)
        else:
            return list1 or list2
        return list1
```
**Tag: 递归、链表**

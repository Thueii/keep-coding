#  合并两个有序链表

Link => [合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)

## 题目

    将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

**示例1**

    输入：l1 = [1,2,4], l2 = [1,3,4]
    输出：[1,1,2,3,4,4]


**执行结果：通过 显示详情**
easy

- 执行用时：24 ms, 在所有 Python3 提交中击败了99.35% 的用户
内存消耗：15 MB, 在所有 Python3 提交中击败了53.72% 的用户
通过测试用例：208 / 208

```python
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(-1)
        p = dummy
        while list1 and list2:
            if list1.val <= list2.val:
                p.next = list1
                list1 = list1.next
            else:
                p.next = list2
                list2 = list2.next
            p = p.next
        p.next = list1 if list1 else list2
        return dummy.next
```

**Tag: 递归、链表**

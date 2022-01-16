#  两数相加 II

Link => [两数相加 II](https://leetcode-cn.com/problems/add-two-numbers-ii/)

## 题目

    给你两个 非空 链表来代表两个非负整数。数字最高位位于链表开始位置。它们的每个节点只存储一位数字。将这两数相加会返回一个新的链表。

    你可以假设除了数字 0 之外，这两个数字都不会以零开头。


**示例1**

    输入：l1 = [7,2,4,3], l2 = [5,6,4]
    输出：[7,8,0,7]


**示例2**

    输入：l1 = [2,4,3], l2 = [5,6,4]
    输出：[8,0,7]



**执行结果：通过 显示详情**
看似很长，但是只能如此

- 执行用时：52 ms, 在所有 Python3 提交中击败了86.43% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了37.50% 的用户
通过测试用例：1563 / 1563

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        list1, list2 = [], []
        while l1:
            list1.append(l1.val)
            l1 = l1.next
        while l2:
            list2.append(l2.val)
            l2 = l2.next
        res_list, remainder = [], 0
        while list1 or list2:
            if not list1:
                tmp = list2.pop()+remainder
            elif not list2:
                tmp = list1.pop()+remainder
            else:
                tmp = list1.pop()+list2.pop()+remainder
            if tmp // 10:
                res_list.append(tmp % 10)
                remainder = 1
            else:
                res_list.append(tmp)
                remainder = 0
        if remainder == 1:
            res_list.append(1)
        dummy = ListNode(0)
        p = dummy
        while res_list:
            tmp = ListNode(res_list.pop())
            p.next = tmp
            p = tmp
        return dummy.next
```

**Tag: 链表、递归、数学**

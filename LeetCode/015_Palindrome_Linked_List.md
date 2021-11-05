# 回文链表

Link => [回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)

给你一个单链表的头节点 head ，请你判断该链表是否为回文链表。如果是，返回 true ；否则，返回 false 。

>输入：head = [1,2,2,1]<br />
>输出：true<br />

执行结果：
通过
显示详情

添加备注
执行用时：576 ms, 在所有 Python3 提交中击败了86.42% 的用户
内存消耗：47.9 MB, 在所有 Python3 提交中击败了30.53% 的用户
通过测试用例：85 / 85

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
        stack =[]
        while head:
            stack.append(head.val)
            head = head.next
        if stack == stack[::-1]:
            return True
        else:
            return False
```
改进：
执行结果：
通过
显示详情

添加备注
执行用时：536 ms, 在所有 Python3 提交中击败了95.35% 的用户
内存消耗：33.1 MB, 在所有 Python3 提交中击败了92.43% 的用户
通过测试用例：85 / 85

其实是计算了一半吧
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
        count = 0
        flag = False
        jishude = head
        while jishude != None:
            jishude = jishude.next
            count += 1
        length = count // 2
        if count % 2 == 1:
            flag = True
        cur = head
        stack = []
        for i in range(length):
            cur_next = cur.next
            cur.next = None
            stack.append(cur)
            cur = cur_next
        if flag == True:
            cur = cur.next
        while cur != None:
            cur_next = cur.next
            cur.next = None
            pop_node = stack.pop()
            if cur.val == pop_node.val:
                cur = cur_next
                continue
            else:
                return False
        return True
```
改进： 
进阶：你能否用 O(n) 时间复杂度和 O(1) 空间复杂度解决此题？

执行结果：
通过
显示详情

添加备注
执行用时：520 ms, 在所有 Python3 提交中击败了96.85% 的用户
内存消耗：32.9 MB, 在所有 Python3 提交中击败了93.04% 的用户
通过测试用例：85 / 85

原地改动，没有使用其他空间
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
        count = 0
        flag = False
        jishude = head
        while jishude != None:
            jishude = jishude.next
            count += 1
        length = count // 2
        if count % 2 == 1:
            flag = True

        pre, cur = None, head
        for i in range(0, length):
            nex = cur.next
            cur.next = pre
            pre = cur
            cur = nex


        if flag:
            cur = cur.next

        while pre and cur:
            if pre.val != cur.val:
                return False
            else:
                pre = pre.next
                cur = cur.next
        return True
```
**Tag: 栈、链表、递归、双指针**

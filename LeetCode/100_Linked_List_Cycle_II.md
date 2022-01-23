# 环形链表 II

Link => [环形链表 II](https://leetcode-cn.com/problems/linked-list-cycle-ii/)

## 题目

    给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

    如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。如果 pos 是 -1，则在该链表中没有环。注意：pos 不作为参数进行传递，仅仅是为了标识链表的实际情况。

    不允许修改 链表。

**示例1**

    输入：head = [3,2,0,-4], pos = 1
    输出：返回索引为 1 的链表节点
    解释：链表中有一个环，其尾部连接到第二个节点。

**示例2**

    输入：head = [1,2], pos = 0
    输出：返回索引为 0 的链表节点
    解释：链表中有一个环，其尾部连接到第一个节点。

**示例3**

    输入：head = [1], pos = -1
    输出：返回 null
    解释：链表中没有环。

**执行结果：通过 显示详情**
哈希实现，很慢

- 执行用时：52 ms, 在所有 Python3 提交中击败了45.01% 的用户
内存消耗：18 MB, 在所有 Python3 提交中击败了18.04% 的用户
通过测试用例：16 / 16

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        # 服了，还是只会哈希表
        adict = {}
        while head:
            if adict.get(head):
                return head
            adict[head] = True
            head = head.next
        return
```
**改进**
快慢指针第二次相遇：[环形链表 II（双指针法，清晰图解）](https://leetcode-cn.com/problems/linked-list-cycle-ii/solution/linked-list-cycle-ii-kuai-man-zhi-zhen-shuang-zhi-/)
- 执行用时：48 ms, 在所有 Python3 提交中击败了70.11% 的用户
内存消耗：17.9 MB, 在所有 Python3 提交中击败了51.01% 的用户
通过测试用例：16 / 16
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        # 我就知道是第几次相遇的，现在终于弄明白了
        slow, fast = head, head # 注意这里是都是head
        while True: # 因为所有的判断都放在下一句最好
            if not (fast and fast.next):
                return
            slow, fast = slow.next, fast.next.next
            if slow == fast:
                break
        fast = head
        while fast != slow:
            fast, slow = fast.next, slow.next
        return fast

```
**2022/01/23**
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        root = head
        slow, fast = head, head
        flag = False
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                flag = True
                break
        if not flag:
            return
        while root:
            if root == slow:
                return slow
            slow = slow.next
            root = root.next
```
**Tag: 哈希表、链表、双指针**

# 环形链表

Link => [环形链表](https://leetcode-cn.com/problems/linked-list-cycle/)

## 题目

    给你一个链表的头节点 head ，判断链表中是否有环。

    如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。如果 pos 是 -1，则在该链表中没有环。注意：pos 不作为参数进行传递，仅仅是为了标识链表的实际情况。

    如果链表中存在环，则返回 true 。 否则，返回 false 。

**示例1**

    输入：head = [3,2,0,-4], pos = 1
    输出：true
    解释：链表中有一个环，其尾部连接到第二个节点。

**示例2**

    输入：head = [1,2], pos = 0
    输出：true
    解释：链表中有一个环，其尾部连接到第一个节点。

**示例3**

    输入：head = [1], pos = -1
    输出：false
    解释：链表中没有环。

**执行结果：通过 显示详情**
我真没意思。。。

- 执行用时：52 ms, 在所有 Python3 提交中击败了65.77% 的用户
内存消耗：18.5 MB, 在所有 Python3 提交中击败了20.56% 的用户
通过测试用例：21 / 21

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        adict = {}
        while head:
            if adict.get(head):
                return True
            else:
                adict[head] = True
            head = head.next
        return False
```
**改进**
快慢指针：
- 难度简单，解题方法古怪，在实际应用中应该没人脑子瓦特用这种方法。

这种古怪的解题方法就是：快慢指针。

快慢指针，顾名思义，是使用速度不同的指针（可用在链表、数组、序列等上面），来解决一些问题。

这些问题主要包括：

    处理环上的问题，比如环形链表、环形数组等。
    需要知道链表的长度或某个特别位置上的信息的时候。

    快慢指针这种算法证明，它们肯定是会相遇的，快的指针一定会追上慢的指针，可以理解成操场上跑步，跑的快的人套圈跑的慢的人。

    一般用 fast 定义快指针，用 slow 定义慢指针。
    速度不同是指 fast 每次多走几步，slow 少走几步。一般设定的都是 fast 走 2 步，slow 走 1 步。

    当然设置成别的整数也是可以的，比如 fast 走 3 步，slow 走 1 步。


- 执行用时：52 ms, 在所有 Python3 提交中击败了65.77% 的用户
内存消耗：18.3 MB, 在所有 Python3 提交中击败了28.12% 的用户
通过测试用例：21 / 21

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        if not head or not head.next:
            return False
        slow, fast = head, head.next
        while fast and fast.next:
            if not fast.next.next:
                return False
            if fast == slow:
                return True
            slow, fast = slow.next, fast.next.next
```
**改进**
当前往前的思路，前缀和+哈希表，巧妙

- 执行用时：64 ms, 在所有 Python3 提交中击败了92.43% 的用户
内存消耗：17.2 MB, 在所有 Python3 提交中击败了36.62% 的用户
通过测试用例：89 / 89

```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        count = {}
        all_sum = 0
        res = 0
        for num in nums:
            all_sum += num
            if all_sum == k:
                res += 1
            if all_sum - k in count:
                res += count[all_sum-k]
            count[all_sum] = count.get(all_sum, 0) + 1
        return res
```
**Tag: 哈希表、链表、双指针**

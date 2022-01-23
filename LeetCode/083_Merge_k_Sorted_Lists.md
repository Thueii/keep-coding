# 合并K个升序链表

Link => [合并K个升序链表](https://leetcode-cn.com/problems/merge-k-sorted-lists/)

## 题目
给你一个链表数组，每个链表都已经按升序排列。

请你将所有链表合并到一个升序链表中，返回合并后的链表。

**示例1**

    输入：lists = [[1,4,5],[1,3,4],[2,6]]
    输出：[1,1,2,3,4,4,5,6]
    解释：链表数组如下：
    [
    1->4->5,
    1->3->4,
    2->6
    ]
    将它们合并到一个有序链表中得到。
    1->1->2->3->4->4->5->6

**示例2**

    输入：lists = []
    输出：[]

**示例3**

    输入：lists = [[]]
    输出：[]


**执行结果：通过 显示详情**
死办法

- 执行用时：72 ms, 在所有 Python3 提交中击败了65.53% 的用户
内存消耗：18.5 MB, 在所有 Python3 提交中击败了23.63% 的用户
通过测试用例：133 / 133

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        all_nums = []
        for each_list in lists:
            root = each_list
            while root:
                all_nums.append(root.val)
                root = root.next
        all_nums.sort()

        res_list = ListNode()
        
        p = res_list

        for i in all_nums:
            tmp = ListNode(i)
            p.next = tmp
            p = p.next

        return res_list.next
```

**改进**
两两合并，原地改变

- 执行用时：2924 ms, 在所有 Python3 提交中击败了20.99% 的用户
内存消耗：17.7 MB, 在所有 Python3 提交中击败了56.93% 的用户
通过测试用例：133 / 133

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        res_list = None

        for each_list in lists:
            if not res_list and each_list:
                res_list = each_list
                continue

            if not res_list or not each_list:
                continue

            if res_list.val < each_list.val:
                res_list = self.mergeTowLists(res_list, each_list)
            else:
                res_list = self.mergeTowLists(each_list, res_list)

        return res_list

    def mergeTowLists(self, list1, list2):
        res = list1
        p = res
        p1 = list1.next
        p2 = list2
        while p1 and p2:
            if p1.val < p2.val:
                p.next = p1
                p1 = p1.next
            else:
                p.next = p2
                p2 = p2.next
            p = p.next
        p.next = p1 if p1 else p2
        return res
```
**改进**
两两合并，新listnode返回

- 执行用时：3004 ms, 在所有 Python3 提交中击败了19.84% 的用户
内存消耗：17.7 MB, 在所有 Python3 提交中击败了59.66% 的用户
通过测试用例：133 / 133

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        res_list = None

        for each_list in lists:
            res_list = self.mergeTowLists(res_list, each_list)

        return res_list

    def mergeTowLists(self, list1, list2):
        res = ListNode()
        p = res
        while list1 and list2:
            if list1.val < list2.val:
                p.next = list1
                list1 = list1.next
                p = p.next
            else:
                p.next = list2
                list2 = list2.next
                p = p.next

        p.next = list1 if list1 else list2

        return res.next
```
**改进**
归并递归，不太理解

- 执行用时：76 ms, 在所有 Python3 提交中击败了58.14% 的用户
内存消耗：17.7 MB, 在所有 Python3 提交中击败了55.06% 的用户
通过测试用例：133 / 133

```python
class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        if not lists: return None
        n = len(lists) #记录子链表数量
        return self.mergeSort(lists, 0, n - 1) #调用归并排序函数
    def mergeSort(self, lists: List[ListNode], l: int, r: int) -> ListNode:
        if l == r:
            return lists[l]
        m = (l + r) // 2
        L = self.mergeSort(lists, l, m) #循环的递归部分
        R = self.mergeSort(lists, m + 1, r)
        return self.mergeTwoLists(L, R) #调用两链表合并函数
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        dummy = ListNode(0) #构造虚节点
        move = dummy #设置移动节点等于虚节点
        while l1 and l2: #都不空时
            if l1.val < l2.val:
                move.next = l1 #移动节点指向数小的链表
                l1 = l1.next
            else:
                move.next = l2
                l2 = l2.next
            move = move.next
        move.next = l1 if l1 else l2 #连接后续非空链表
        return dummy.next #虚节点仍在开头
```

**改进**
最快的还是最小堆
- 执行用时：64 ms, 在所有 Python3 提交中击败了82.95% 的用户
内存消耗：18.5 MB, 在所有 Python3 提交中击败了26.34% 的用户
通过测试用例：133 / 133

```python
class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        import heapq #调用堆
        minHeap = []
        for listi in lists: 
            while listi:
                heapq.heappush(minHeap, listi.val) #把listi中的数据逐个加到堆中
                listi = listi.next
        dummy = ListNode(0) #构造虚节点
        p = dummy
        while minHeap:
            p.next = ListNode(heapq.heappop(minHeap)) #依次弹出最小堆的数据
            p = p.next
        return dummy.next 
```
**2022/01/23**
```python
class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        import heapq
        stack = []
        for listi in lists:
            while listi:
                heapq.heappush(stack, listi.val)
                listi = listi.next
        dummy = ListNode(-1)
        cur = dummy
        while stack:
            tmp = ListNode(heapq.heappop(stack))
            cur.next = tmp
            cur = tmp
        return dummy.next
```
**Tag: 链表、分治、堆、归并排序**

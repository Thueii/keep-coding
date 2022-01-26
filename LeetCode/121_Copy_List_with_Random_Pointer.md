# 复制带随机指针的链表

Link => [复制带随机指针的链表](https://leetcode-cn.com/problems/copy-list-with-random-pointer/)

## 题目

    给你一个长度为 n 的链表，每个节点包含一个额外增加的随机指针 random ，该指针可以指向链表中的任何节点或空节点。

    构造这个链表的 深拷贝。 深拷贝应该正好由 n 个 全新 节点组成，其中每个新节点的值都设为其对应的原节点的值。新节点的 next 指针和 random 指针也都应指向复制链表中的新节点，并使原链表和复制链表中的这些指针能够表示相同的链表状态。复制链表中的指针都不应指向原链表中的节点 。

    例如，如果原链表中有 X 和 Y 两个节点，其中 X.random --> Y 。那么在复制链表中对应的两个节点 x 和 y ，同样有 x.random --> y 。

    返回复制链表的头节点。

    用一个由 n 个节点组成的链表来表示输入/输出中的链表。每个节点用一个 [val, random_index] 表示：

        val：一个表示 Node.val 的整数。
        random_index：随机指针指向的节点索引（范围从 0 到 n-1）；如果不指向任何节点，则为  null 。

    你的代码 只 接受原链表的头节点 head 作为传入参数。


**示例1**

    输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
    输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]

**示例2**

    输入：head = [[1,1],[2,1]]
    输出：[[1,1],[2,1]]


**执行结果：通过 显示详情**
哈希做的，常规办法

- 执行用时：36 ms, 在所有 Python3 提交中击败了72.58% 的用户
内存消耗：15.7 MB, 在所有 Python3 提交中击败了48.42% 的用户
通过测试用例：19 / 19v

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random
"""

class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        hash_node = {}
        new_idx = {}
        count = 0
        root = head
        dummy = Node(-1)
        pre = dummy
        while head:
            hash_node[head] = count
            tmp = Node(head.val)
            pre.next = tmp
            new_idx[count] = tmp
            pre = pre.next

            count += 1
            head = head.next
        idx = 0
        while root:
            new_idx[hash_node[root]].random = new_idx[hash_node[root.random]] if root.random else None
            root = root.next
        return dummy.next
```
**改进**
像DNA复制一样，把新节点穿在老节点后面
- 执行用时：40 ms, 在所有 Python3 提交中击败了46.34% 的用户
内存消耗：15.7 MB, 在所有 Python3 提交中击败了48.80% 的用户

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random
"""

class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        if not head:
            return head
            
        p1 = p2 = p3 = head
        while p1:
            new_node = Node(p1.val)
            new_node.next = p1.next
            p1.next = new_node
            p1 = new_node.next
        
        while p2:
            if p2.random:
                p2.next.random = p2.random.next
            p2 = p2.next.next

        new_head = p3.next
        while p3:
            nxt = p3.next.next
            if nxt:
                p3.next.next = nxt.next
            p3 = nxt
        return new_head
```
**Tag: 链表、哈希表**

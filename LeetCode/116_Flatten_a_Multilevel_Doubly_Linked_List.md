# 扁平化多级双向链表

Link => [扁平化多级双向链表](https://leetcode-cn.com/problems/flatten-a-multilevel-doubly-linked-list/)

## 题目

    多级双向链表中，除了指向下一个节点和前一个节点指针之外，它还有一个子链表指针，可能指向单独的双向链表。这些子列表也可能会有一个或多个自己的子项，依此类推，生成多级数据结构，如下面的示例所示。

    给你位于列表第一级的头节点，请你扁平化列表，使所有结点出现在单级双链表中。

**示例1**

    输入：head = [1,2,3,4,5,6,null,null,null,7,8,9,10,null,null,11,12]
    输出：[1,2,3,7,8,11,12,9,10,4,5,6]

**示例2**

    输入：head = [1,2,null,3]
    输出：[1,3,2]

**执行结果：通过 显示详情**
双向链表注意

- 执行用时：32 ms, 在所有 Python3 提交中击败了88.17% 的用户
内存消耗：15.7 MB, 在所有 Python3 提交中击败了49.42% 的用户
通过测试用例：26 / 26

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val, prev, next, child):
        self.val = val
        self.prev = prev
        self.next = next
        self.child = child
"""

class Solution:
    def flatten(self, head: 'Node') -> 'Node':
        root = head
        stack = []
        while head:
            if head.child:
                if head.next:
                    head.next.prev = None
                    stack.append(head.next)
                head.next = head.child
                head.child.prev = head
                head.child = None
                head = head.next
            else:
                if head.next:
                    head = head.next
                else:
                    if stack:
                        head.next = stack.pop()
                        head.next.prev = head
                        head = head.next
                    else:
                        head = head.next
        return root
```
**递归**
```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val, prev, next, child):
        self.val = val
        self.prev = prev
        self.next = next
        self.child = child
"""

class Solution:
    def flatten(self, head: 'Node') -> 'Node':
        # 递归
        def dfs(node):
            if not node:
                return node
            if node.child:
                last = dfs(node.child)
                if last:
                    last.next = node.next
                if node.next:
                    node.next.prev = last
                node.next = node.child
                node.child.prev = node
                node.child = None
                return dfs(last)
            elif not node.next and not node.child: # 注意
                return node
            else:
                return dfs(node.next)

        dfs(head)
        return head     
```
**迭代**
一遍过啊~~~~
```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val, prev, next, child):
        self.val = val
        self.prev = prev
        self.next = next
        self.child = child
"""

class Solution:
    def flatten(self, head: 'Node') -> 'Node':
        # 迭代
        cur = head
        while cur:
            if not cur.child:
                cur = cur.next
            else:
                sub_node = cur.child
                while sub_node and sub_node.next:
                    sub_node = sub_node.next
                sub_node.next = cur.next
                if cur.next:
                    cur.next.prev = sub_node
                cur.next = cur.child
                cur.next.prev = cur
                cur.child = None
                cur = cur.next
        return head
```
**Tag: 深度优先搜索、链表、双向链表**

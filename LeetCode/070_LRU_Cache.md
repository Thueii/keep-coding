# LRU 缓存

Link => [LRU 缓存](https://leetcode-cn.com/problems/lru-cache/)

## 题目
请你设计并实现一个满足  LRU (最近最少使用) 缓存 约束的数据结构。
实现 LRUCache 类：

    LRUCache(int capacity) 以 正整数 作为容量 capacity 初始化 LRU 缓存
    int get(int key) 如果关键字 key 存在于缓存中，则返回关键字的值，否则返回 -1 。
    void put(int key, int value) 如果关键字 key 已经存在，则变更其数据值 value ；如果不存在，则向缓存中插入该组 key-value 。如果插入操作导致关键字数量超过 capacity ，则应该 逐出 最久未使用的关键字。

函数 get 和 put 必须以 O(1) 的平均时间复杂度运行。

**示例1**
>输入：["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]<br />
>输出：[null, null, null, 1, null, -1, null, -1, 3, 4]<br />

**执行结果：通过 显示详情**
只是先写出来，完全没有达到：函数 get 和 put 必须以 O(1) 的平均时间复杂度运行。

- 执行用时：2316 ms, 在所有 Python3 提交中击败了10.31% 的用户
内存消耗：72 MB, 在所有 Python3 提交中击败了25.84% 的用户
通过测试用例：22 / 22

```python
class LRUCache:

    def __init__(self, capacity: int):
        self.lookup = {}
        self.capacity = capacity
        self.alist = []

    def get(self, key: int) -> int:
        if key in self.lookup:
            self.alist.append(self.alist.pop(self.alist.index(key)))
            return self.lookup[key]
        else:
            return -1

    def put(self, key: int, value: int) -> None:
        if key in self.lookup:
            self.lookup[key] = value
            self.alist.append(self.alist.pop(self.alist.index(key)))
        else:
            if self.capacity > 0:
                self.lookup[key] = value
                self.alist.append(key)
                self.capacity -= 1
            else:
                _key = self.alist.pop(0)
                self.lookup[key] = value
                self.alist.append(key)
                del self.lookup[_key]


# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```
**改进**
双向链表，第一次尝试，前后顺序很重要，要不然就全盘皆输，最好先处理新节点，这样不改变原来的东西，再改变原来的链路

- 执行用时：616 ms, 在所有 Python3 提交中击败了39.26% 的用户
内存消耗：71.4 MB, 在所有 Python3 提交中击败了72.73% 的用户
通过测试用例：22 / 22

```python
class ListNode:
    def __init__(self, key=None, value=None):
        self.key = key
        self.value = value
        self.prev = None
        self.next = None

class LRUCache:

    def __init__(self, capacity: int):
        self.capacity = capacity
        self.hashmap = {}

        self.head = ListNode()
        self.tail = ListNode()

        self.head.next = self.tail
        self.tail.prev = self.head

    def get(self, key: int) -> int:
        if key in self.hashmap:
            self.hashmap[key].prev.next = self.hashmap[key].next
            self.hashmap[key].next.prev = self.hashmap[key].prev

            self.hashmap[key].prev = self.tail.prev
            self.hashmap[key].next = self.tail
            self.tail.prev.next = self.hashmap[key]
            self.tail.prev = self.hashmap[key]

            return self.hashmap[key].value
        else:
            return -1

    def put(self, key: int, value: int) -> None:
        if key in self.hashmap:
            self.hashmap[key].value = value

            self.hashmap[key].prev.next = self.hashmap[key].next
            self.hashmap[key].next.prev = self.hashmap[key].prev

            self.hashmap[key].prev = self.tail.prev
            self.hashmap[key].next = self.tail
            self.tail.prev.next = self.hashmap[key]
            self.tail.prev = self.hashmap[key]
        else:
            

            if self.capacity > 0:
                self.capacity -= 1
            else:
                self.hashmap.pop(self.head.next.key)
                self.head.next = self.head.next.next
                self.head.next.prev = self.head

            new = ListNode(key, value)
            self.hashmap[key] = new
            new.next = self.tail
            new.prev = self.tail.prev
            self.tail.prev.next = new
            self.tail.prev = new

# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```

**改进**
封装一下

- 执行用时：576 ms, 在所有 Python3 提交中击败了73.20% 的用户
内存消耗：71.4 MB, 在所有 Python3 提交中击败了59.31% 的用户
通过测试用例：22 / 22

```python
class ListNode:
    def __init__(self, key=None, value=None):
        self.key = key
        self.value = value
        self.prev = None
        self.next = None


class LRUCache:
    def __init__(self, capacity: int):
        self.capacity = capacity
        self.hashmap = {}
        # 新建两个节点 head 和 tail
        self.head = ListNode()
        self.tail = ListNode()
        # 初始化链表为 head <-> tail
        self.head.next = self.tail
        self.tail.prev = self.head

    # 因为get与put操作都可能需要将双向链表中的某个节点移到末尾，所以定义一个方法
    def move_node_to_tail(self, key):
            # 先将哈希表key指向的节点拎出来，为了简洁起名node
            #      hashmap[key]                               hashmap[key]
            #           |                                          |
            #           V              -->                         V
            # prev <-> node <-> next         pre <-> next   ...   node
            node = self.hashmap[key]
            node.prev.next = node.next
            node.next.prev = node.prev
            # 之后将node插入到尾节点前
            #                 hashmap[key]                 hashmap[key]
            #                      |                            |
            #                      V        -->                 V
            # prev <-> tail  ...  node                prev <-> node <-> tail
            node.prev = self.tail.prev
            node.next = self.tail
            self.tail.prev.next = node
            self.tail.prev = node

    def get(self, key: int) -> int:
        if key in self.hashmap:
            # 如果已经在链表中了久把它移到末尾（变成最新访问的）
            self.move_node_to_tail(key)
        res = self.hashmap.get(key, -1)
        if res == -1:
            return res
        else:
            return res.value

    def put(self, key: int, value: int) -> None:
        if key in self.hashmap:
            # 如果key本身已经在哈希表中了就不需要在链表中加入新的节点
            # 但是需要更新字典该值对应节点的value
            self.hashmap[key].value = value
            # 之后将该节点移到末尾
            self.move_node_to_tail(key)
        else:
            if len(self.hashmap) == self.capacity:
                # 去掉哈希表对应项
                self.hashmap.pop(self.head.next.key)
                # 去掉最久没有被访问过的节点，即头节点之后的节点
                self.head.next = self.head.next.next
                self.head.next.prev = self.head
            # 如果不在的话就插入到尾节点前
            new = ListNode(key, value)
            self.hashmap[key] = new
            new.prev = self.tail.prev
            new.next = self.tail
            self.tail.prev.next = new
            self.tail.prev = new
```
**Tag: 递归、字符串、动态规划**

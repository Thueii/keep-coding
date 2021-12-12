# 实现 Trie (前缀树)

Link => [实现 Trie (前缀树)](https://leetcode-cn.com/problems/implement-trie-prefix-tree/)

## 题目
Trie（发音类似 "try"）或者说 前缀树 是一种树形数据结构，用于高效地存储和检索字符串数据集中的键。这一数据结构有相当多的应用情景，例如自动补完和拼写检查。

请你实现 Trie 类：

    Trie() 初始化前缀树对象。
    void insert(String word) 向前缀树中插入字符串 word 。
    boolean search(String word) 如果字符串 word 在前缀树中，返回 true（即，在检索之前已经插入）；否则，返回 false 。
    boolean startsWith(String prefix) 如果之前已经插入的字符串 word 的前缀之一为 prefix ，返回 true ；否则，返回 false 。

**示例1**
>输入：["Trie", "insert", "search", "search", "startsWith", "insert", "search"][[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]<br />
>输出：[null, null, true, false, true, null, true]<br />
>解释：<br />
Trie trie = new Trie();<br />
trie.insert("apple");<br />
trie.search("apple");   // 返回 True<br />
trie.search("app");     // 返回 False<br />
trie.startsWith("app"); // 返回 True<br />
trie.insert("app");<br />
trie.search("app");     // 返回 True<br />

**执行结果：通过 显示详情**
知道肯定不对，因为不会，只能这么写了

- 执行用时：980 ms, 在所有 Python3 提交中击败了5.09% 的用户
内存消耗：21.3 MB, 在所有 Python3 提交中击败了95.12% 的用户
通过测试用例：15 / 15

```python
class Trie:

    def __init__(self):
        self.dic = set()

    def insert(self, word: str) -> None:
        self.dic.add(word)

    def search(self, word: str) -> bool:
        return True if word in self.dic else False

    def startsWith(self, prefix: str) -> bool:
        for i in self.dic:
            if len(i) < len(prefix):
                continue
            if i[:len(prefix)] == prefix:     
                return True
        return False



# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```
**这样才对**
字典树，终于看到一个简单写法，复杂的真的看的不是很明白= =

- 执行用时：92 ms, 在所有 Python3 提交中击败了98.04% 的用户
内存消耗：27.7 MB, 在所有 Python3 提交中击败了83.48% 的用户
通过测试用例：15 / 15

```python
# 空手一次写成功，理解了
class Trie:

    def __init__(self):
        self.lookup = {}

    def insert(self, word: str) -> None:
        cur = self.lookup
        for i in word:
            if i not in cur:
                cur[i] = {}
            cur = cur[i]
        cur["flag"] = True  # 标志它是一个存在的单词

    def search(self, word: str) -> bool:
        cur = self.lookup
        for i in word:
            if i not in cur:
                return False
            cur = cur[i]
        return "flag" in cur

    def startsWith(self, prefix: str) -> bool:
        cur = self.lookup
        for i in prefix:
            if i not in cur:
                return False
            cur = cur[i]
        return True



# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```
**Tag: 字典树、字符串、设计、哈希表**

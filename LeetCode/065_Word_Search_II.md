# 单词搜索 II

Link => [单词搜索 II](https://leetcode-cn.com/problems/word-search-ii/)

## 题目
给定一个 m x n 二维字符网格 board 和一个单词（字符串）列表 words，找出所有同时在二维网格和字典中出现的单词。

单词必须按照字母顺序，通过 相邻的单元格 内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母在一个单词中不允许被重复使用。

**示例1**
>输入：board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]<br />
>输出：["eat","oath"]<br />

**执行结果：通过 显示详情**
写的是可以实现的，但是超过时间限制。。伤心，好不容易写出来哈哈

- 超出时间限制

```python
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

class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:

        atrie = Trie()
        for word in words:
            atrie.insert(word)

        res = set()
        max_h = len(board[0])
        max_w = len(board)

        preset = set()
        inset = set()
        def find_w(w, h, now):
            if h < max_h and h >= 0 and w < max_w and w >= 0:
                if board[w][h] and (now+board[w][h] in preset or atrie.startsWith(now+board[w][h])):
                    cur = now+board[w][h]
                    preset.add(cur)
                    if cur in inset or atrie.search(cur):
                        inset.add(cur)
                        res.add(cur)
                    tmp = board[w][h]
                    board[w][h] = False
                    find_w(w, h+1, now+tmp)
                    find_w(w, h-1, now+tmp)
                    find_w(w+1, h, now+tmp)
                    find_w(w-1, h, now+tmp)
                    board[w][h] = tmp


        for i in range(len(board)):
            for j in range(len(board[i])):
                find_w(i, j, "")

        return list(res)
```
**这样才对**
！！！！！剪枝外加前缀树的最后的标志直接标记成单词！

- 执行用时：5088 ms, 在所有 Python3 提交中击败了34.19% 的用户
内存消耗：17 MB, 在所有 Python3 提交中击败了11.08% 的用户
通过测试用例：62 / 62

```python
class Trie:
    def __init__(self):
        self.root = TreeNode('')

    def insert(self, word):
        p = self.root
        for char in word:
            if char not in p.child:
                p.child[char] = TreeNode(char)
            p = p.child[char]
        p.word = word

class TreeNode:
    def __init__(self, value):
        self.val = value
        self.child = {}
        self.word = None

class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:

        atrie = Trie()
        for word in words:
            atrie.insert(word)

        res = set()
        max_w = len(board)
        max_h = len(board[0])

        def find_w(w, h, root):
            if w < 0 or w >= max_w or h < 0 or h >= max_h:
                return

            if board[w][h] not in root.child:
                return
            if root.child[board[w][h]].word:
                res.add(root.child[board[w][h]].word)
                root.child[board[w][h]].word = False

            tmp = board[w][h]
            board[w][h] = "*"
            find_w(w, h+1, root.child[tmp])
            find_w(w, h-1, root.child[tmp])
            find_w(w+1, h, root.child[tmp])
            find_w(w-1, h, root.child[tmp])
            board[w][h] = tmp

        for i in range(len(board)):
            for j in range(len(board[0])):
                find_w(i, j, atrie.root)

        return list(res)
```
**Tag: 字典树、数组、字符串、回溯、矩阵**

# 词典中最长的单词

Link => [词典中最长的单词](https://leetcode-cn.com/problems/longest-word-in-dictionary/)

## 题目
给出一个字符串数组words组成的一本英语词典。从中找出最长的一个单词，该单词是由words词典中其他单词逐步添加一个字母组成。若其中有多个可行的答案，则返回答案中字典序最小的单词。

若无答案，则返回空字符串。

**示例1**
>输入：words = ["w","wo","wor","worl", "world"]<br />
>输出："world"<br />
>解释：单词"world"可由"w", "wo", "wor", 和 "worl"添加一个字母组成。<br />

**示例2**
>输入：words = ["a", "banana", "app", "appl", "ap", "apply", "apple"]<br />
>输出："apple"<br />
>解释："apply"和"apple"都能由词典中的单词组成。但是"apple"的字典序小于"apply"。<br />

**执行结果：通过 显示详情**
是因为递归所以太慢了吗

- 执行用时：152 ms, 在所有 Python3 提交中击败了14.11% 的用户
内存消耗：17.6 MB, 在所有 Python3 提交中击败了5.03% 的用户
通过测试用例：59 / 59

```python
class Solution:
    def longestWord(self, words: List[str]) -> str:
        adict = {}
        for i in words:
            if not adict.get(i):
                adict[i] = True
        
        def is_in(s):
            if len(s)<=1:
                return True
            if s[:-1:] in adict and is_in(s[:-1:]):
                return True
            return False

        res = ""
        for i in adict.keys():
            if is_in(i):
                if len(i) > len(res) or (len(i) == len(res) and i < res):
                    res = i
        return res
```
**改进**
晕菜了 我不知道为什么想到并查集，试了一下 也没有很快 ，稍好一些

- 执执行用时：64 ms, 在所有 Python3 提交中击败了43.02% 的用户
内存消耗：15.3 MB, 在所有 Python3 提交中击败了79.61% 的用户
通过测试用例：59 / 59
```python
class UnionFind:
    def __init__(self):
        self.father = {}
    
    def add(self, x):
        if x not in self.father:
            self.father[x] = None

    def find(self, x):
        root = x
        while self.father[root]:
            root = self.father[root]
        while x != root:
            next_father = self.father[x]
            self.father[x] = root
            x = next_father
        return root
    
    def merge(self, a):
        root_a = a
        if len(a)>1 and a[:-1:] in self.father:
            root_b = self.find(a[:-1:])
            self.father[root_a] = root_b

class Solution:
    def longestWord(self, words: List[str]) -> str:
        words.sort()
        uf = UnionFind()
        for word in words:
            uf.add(word)
            uf.merge(word)

        res = ""
        for word in words:
            if len(uf.find(word)) == 1:
                if len(word) > len(res) or (len(word) == len(res) and word < res):
                    res = word
        return res
```
**改进**
字典树，如果只要判断村不存在，用一个set来保存状态也是很好的

- 执行用时：44 ms, 在所有 Python3 提交中击败了75.98% 的用户
内存消耗：15.4 MB, 在所有 Python3 提交中击败了45.67% 的用户
通过测试用例：59 / 59

```python
class Solution:
    def longestWord(self, words: List[str]) -> str:
        adict = {}
        words.sort()
        res = ""
        for i in words:
            if len(i) == 1 or i[:-1:] in adict:
                adict[i] = True
                if len(i) > len(res) or (len(i) == len(res) and i < res):
                    res = i
        return res
```
**Tag: 字典树、数组、哈希表、字符串、排序**

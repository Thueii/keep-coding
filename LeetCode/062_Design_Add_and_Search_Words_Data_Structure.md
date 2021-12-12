# 添加与搜索单词 - 数据结构设计

Link => [添加与搜索单词 - 数据结构设计](https://leetcode-cn.com/problems/design-add-and-search-words-data-structure/)

## 题目
请你设计一个数据结构，支持 添加新单词 和 查找字符串是否与任何先前添加的字符串匹配 。

实现词典类 WordDictionary ：

    WordDictionary() 初始化词典对象
    void addWord(word) 将 word 添加到数据结构中，之后可以对它进行匹配
    bool search(word) 如果数据结构中存在字符串与 word 匹配，则返回 true ；否则，返回  false 。word 中可能包含一些 '.' ，每个 . 都可以表示任何一个字母。

**示例1**
>输入：["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
[[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]<br />
>输出：[null,null,null,null,false,true,true,true]<br />
>解释：<br />
>WordDictionary wordDictionary = new WordDictionary();<br />
>wordDictionary.addWord("bad");<br />
>wordDictionary.addWord("dad");<br />
>wordDictionary.addWord("mad");<br />
>wordDictionary.search("pad"); // return False<br />
>wordDictionary.search("bad"); // return True<br />
>wordDictionary.search(".ad"); // return True<br />
>wordDictionary.search("b.."); // return True<br />

**执行结果：通过 显示详情**
这个还是挺简单的

- 执行用时：108 ms, 在所有 Python3 提交中击败了93.77% 的用户
内存消耗：23.6 MB, 在所有 Python3 提交中击败了89.94% 的用户
通过测试用例：13 / 13

```python
class WordDictionary:

    def __init__(self):
        self.adict = collections.defaultdict(list)

    def addWord(self, word: str) -> None:
        self.adict[len(word)].append(word)

    def search(self, word: str) -> bool:
        if word in self.adict[len(word)]:
            return True

        pos = {}
        for i in range(len(word)):  # 把不是.的位置找出来
            if word[i] != ".":
                pos[i] = word[i]

        if self.adict.get(len(word)):
            for i in self.adict[len(word)]:
                for p, word in pos.items():
                    if i[p] != word:
                        break
                else:
                    return True

        return False
        


# Your WordDictionary object will be instantiated and called as such:
# obj = WordDictionary()
# obj.addWord(word)
# param_2 = obj.search(word)
```
**Tag: 深度优先搜索、字典树、字符串、设计**

# 单词替换

Link => [单词替换](https://leetcode-cn.com/problems/replace-words/)

## 题目
在英语中，我们有一个叫做 词根(root)的概念，它可以跟着其他一些词组成另一个较长的单词——我们称这个词为 继承词(successor)。例如，词根an，跟随着单词 other(其他)，可以形成新的单词 another(另一个)。

现在，给定一个由许多词根组成的词典和一个句子。你需要将句子中的所有继承词用词根替换掉。如果继承词有许多可以形成它的词根，则用最短的词根替换它。

你需要输出替换之后的句子。

**示例1**
>输入：dictionary = ["cat","bat","rat"], sentence = "the cattle was rattled by the battery"<br />
>输出："the cat was rat by the bat"<br />

**执行结果：通过 显示详情**
想法很简单，按开头字母做索引，然后逐个匹配字母以下的内容，感觉缺那么点感觉，还是看看题解

- 执行用时：44 ms, 在所有 Python3 提交中击败了97.77% 的用户
内存消耗：18.8 MB, 在所有 Python3 提交中击败了83.17% 的用户
通过测试用例：126 / 126

```python
class Solution:
    def replaceWords(self, dictionary: List[str], sentence: str) -> str:
        adict = collections.defaultdict(list) # 前缀字典
        for i in dictionary:
            adict[i[0]].append(i)
        for k, v in adict.items():
            adict[k].sort()

        sentence = sentence.split(" ")
        for i in range(len(sentence)): # 遍历字典
            if adict.get(sentence[i][0]):
                for j in adict[sentence[i][0]]:
                    if j in sentence[i] and sentence[i].index(j) == 0: # 前缀匹配 也可以换成是.starstwith(j)
                        sentence[i] = j
                        break
        return " ".join(sentence)
```
**Tag: 深度优先搜索、字典树、字符串、设计**

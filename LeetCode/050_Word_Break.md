# 单词拆分

Link => [单词拆分](https://leetcode-cn.com/problems/word-break/)

## 题目
给你一个字符串 s 和一个字符串列表 wordDict 作为字典，判定 s 是否可以由空格拆分为一个或多个在字典中出现的单词。

说明：拆分时可以重复使用字典中的单词。

**示例1**
>输入：s = "leetcode", wordDict = ["leet", "code"]<br />
>输出：true<br />
>说明：返回 true 因为 "leetcode" 可以被拆分成 "leet code"。<br />

**示例2**
>输入：s = "applepenapple", wordDict = ["apple", "pen"]<br />
>输出：true<br />
>说明：返回 true 因为 "applepenapple" 可以被拆分成 "apple pen apple"。
     注意你可以重复使用字典中的单词。<br />

**执行结果：通过 显示详情**
写得好烂，再想想

- 执行用时：484 ms, 在所有 Python3 提交中击败了5.95% 的用户
内存消耗：17.2 MB, 在所有 Python3 提交中击败了5.04% 的用户
通过测试用例：45 / 45
```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        in_dict = {}
        for i in wordDict:
            in_dict[i] = True

        not_dict = {}

        def find(s, wordDict):
            if in_dict.get(s):
                return True
            elif not_dict.get(s):
                return False
            if len(s) == 1:
                return False

            index = 1
            while index < len(s):
                if find(s[:index], wordDict) and find(s[index::], wordDict):
                    in_dict[s] = True
                    return True
                else:
                    not_dict[s] = True
                    index += 1
            return False

        return find(s, wordDict)


```
**改进：**
动态规划。。。好久不用就不会了

- 执行用时：32 ms, 在所有 Python3 提交中击败了93.57% 的用户
内存消耗：15 MB, 在所有 Python3 提交中击败了73.37% 的用户
通过测试用例：45 / 45

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:       
        n=len(s)
        dp=[False]*(n+1)
        dp[0]=True
        for i in range(n):
            for j in range(i+1,n+1):
                # 若 dp[i]=Truedp[i]=Truedp[i]=True 且 s[i,⋯ ,j)s[i,\cdots,j)s[i,⋯,j) 
                # 在 wordlistwordlistwordlist 中：dp[j]=Truedp[j]=Truedp[j]=True。
                # 解释：dp[i]=Truedp[i]=Truedp[i]=True 说明 sss 的前 iii 位可以用 
                # wordDictwordDictwordDict 表示，则 s[i,⋯ ,j)s[i,\cdots,j)s[i,⋯,j) 
                # 出现在 wordDictwordDictwordDict 中，说明 sss 的前 jjj 位可以表示。
                if(dp[i] and (s[i:j] in wordDict)):
                    dp[j]=True
        return dp[-1]
```
**改进：**
记忆化搜索
看到这个我才明白为啥我自己写的很慢，我前面的东西很多重复做了，像这里只做了一半就节省了很多
但是不加语法糖其实很慢，动态规划还要多理解一下

- 执行用时：40 ms, 在所有 Python3 提交中击败了58.58% 的用户
内存消耗：15.2 MB, 在所有 Python3 提交中击败了14.52% 的用户
通过测试用例：45 / 45
```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        import functools
        @functools.lru_cache(None)
        def find(s):
            if not s:
                return True

            for i in range(1, len(s) + 1):
                if (s[:i] in wordDict) and find(s[i::]): # 我的前半部分又重复做了
                    return True
            return False

        return find(s)
```
**改进：**
根据上面的启发把我自己的代码改了一下
我等于自己做了记忆化，但是还是没有动态规划好
而且看起来很乱

- 执行用时：36 ms, 在所有 Python3 提交中击败了80.66% 的用户
内存消耗：15.5 MB, 在所有 Python3 提交中击败了5.04% 的用户
通过测试用例：45 / 45
```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        in_dict = {}
        for i in wordDict:
            in_dict[i] = True

        not_dict = {}

        def find(s):
            nonlocal in_dict, not_dict
            if in_dict.get(s):
                return True
            elif not_dict.get(s):
                return False
            if len(s) == 1:
                not_dict[s] = True
                return False

            index = 1
            while index < len(s):
                if s[:index] in in_dict and find(s[index::]):  # 减少一半
                    in_dict[s] = True
                    return True
                else:
                    not_dict[s] = True
                    index += 1
            not_dict[s] = True
            return False

        return find(s)
```
**Tag: 字典树、记忆化搜索、哈希表、字符串、动态规划**

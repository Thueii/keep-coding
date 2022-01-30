# 电话号码的字母组合

Link => [电话号码的字母组合](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)

## 题目
给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。答案可以按 任意顺序 返回。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

**示例1**

    输入：digits = "23"
    输出：["ad","ae","af","bd","be","bf","cd","ce","cf"]

**示例2**

    输入：digits = ""
    输出：[]

**执行结果：通过 显示详情**
基本方法

- 执行用时：28 ms, 在所有 Python3 提交中击败了87.59% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了30.71% 的用户
通过测试用例：25 / 25

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        num_char = dict()
        num_char['2'] = ['a','b','c']
        num_char['3'] = ['d','e','f']
        num_char['4'] = ['g','h','i']
        num_char['5'] = ['j','k','l']
        num_char['6'] = ['m','n','o']
        num_char['7'] = ['p','q','r','s']
        num_char['8'] = ['t','u','v']
        num_char['9'] = ['w','x','y','z']

        digits_list = []
        for i in digits:
            digits_list.append(i)

        def dfs(cur_res, left_nums):
            if not left_nums:
                res.append(cur_res)
                return
            tmp = left_nums.pop()
            char_list = num_char[tmp]
            for i in char_list:
                dfs(cur_res + i, left_nums)
            left_nums.append(tmp)

        if digits == "":
            return []
        
        res = []

        dfs("", digits_list[::-1])
        return res
```
**改进：**
瞬间感觉自己太死板了

- 执行用时：32 ms, 在所有 Python3 提交中击败了64.45% 的用户
内存消耗：15.2 MB, 在所有 Python3 提交中击败了5.53% 的用户
通过测试用例：25 / 25

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        # 边界 
        if len(digits) == 0:
            return list()
        # 回溯算法
        num_char = dict()
        num_char['2'] = ['a','b','c']
        num_char['3'] = ['d','e','f']
        num_char['4'] = ['g','h','i']
        num_char['5'] = ['j','k','l']
        num_char['6'] = ['m','n','o']
        num_char['7'] = ['p','q','r','s']
        num_char['8'] = ['t','u','v']
        num_char['9'] = ['w','x','y','z']

        # 初始化
        self.ans = list()
        self.path = list()
        
        # 回溯算法
        def back_tracking(index):
            if len(self.path) == len(digits):
                # 保留结果
                self.ans.append("".join(self.path[:]))
                return 
            for char in num_char[digits[index]]:
                self.path.append(char)
                back_tracking(index+1)
                self.path.pop()
        # 调用
        back_tracking(0)

        return self.ans

```
**2022/01/30**
```python
# 回溯
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if digits == "":
            return []
        #数字对应的英文字母列表
        word_list = {
            "2":"abc", 
            "3":"def",
            "4": "ghi",
            "5": "jkl",
            "6": "mno",
            "7": "pqrs",
            "8": "tuv",
            "9": "wxyz"
        }
        res = []
        def dfs(left_num, now):
            if len(left_num) == 0:
                res.append(now[:])
                return
            for i in word_list[left_num[0]]:
                dfs(left_num[1:], now+i)
        dfs(digits, "")
        return res
```
```python
# 迭代
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        #数字对应的英文字母列表
        word_list = ["0", "0", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"]

        res = []
        for num in digits:
            tmp = []
            now_word_list = word_list[int(num)]
            if res:
                for i in now_word_list:
                    for j in res:
                        tmp.append(j+i)
            else:
                for i in now_word_list:
                    tmp.append(i)
            res = tmp
        return res
```
**Tag: 哈希表、字符串、回溯**

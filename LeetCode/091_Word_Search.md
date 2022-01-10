# 单词搜索

Link => [单词搜索](https://leetcode-cn.com/problems/word-search/)

## 题目

    给定一个 m x n 二维字符网格 board 和一个字符串单词 word 。如果 word 存在于网格中，返回 true ；否则，返回 false 。

    单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。


**示例1**

    输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
    输出：true


**示例2**

    输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
    输出：true

**执行结果：通过 显示详情**
出息了

- 执行用时：2676 ms, 在所有 Python3 提交中击败了93.96% 的用户
内存消耗：15.2 MB, 在所有 Python3 提交中击败了37.50% 的用户
通过测试用例：83 / 83

```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        max_x = len(board)
        max_y = len(board[0])

        def dfs(cur_board, posx, posy, left_word):
            # print(cur_board)
            if cur_board[posx][posy] == left_word[-1]:
                tmp = cur_board[posx][posy]
                cur_board[posx][posy] = ""
                tmp2 = left_word.pop()

                if not left_word:
                    return True

                if posy - 1 >= 0:
                    if dfs(cur_board, posx, posy - 1, left_word):
                        return True
                if posy + 1 < max_y:
                    if dfs(cur_board, posx, posy + 1, left_word):
                        return True
                if posx + 1 < max_x:
                    if dfs(cur_board, posx + 1, posy, left_word):
                        return True
                if posx - 1 >= 0:
                    if dfs(cur_board, posx - 1, posy, left_word):
                        return True
                cur_board[posx][posy] = tmp
                left_word.append(tmp2)
            return

        word = word[::-1]
        word_list = []
        for i in word:
            word_list.append(i)
        for i in range(max_x):
            for j in range(max_y):
                if board[i][j] == word[-1]:
                    if dfs(board, i, j, word_list):
                        return True
        return False
```

**Tag: 数组、回溯、矩阵**

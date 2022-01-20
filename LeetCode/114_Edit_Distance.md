# 编辑距离

Link => [编辑距离](https://leetcode-cn.com/problems/edit-distance/)

## 题目

给你两个单词 word1 和 word2，请你计算出将 word1 转换成 word2 所使用的最少操作数 。

你可以对一个单词进行如下三种操作：

    插入一个字符
    删除一个字符
    替换一个字符

**示例1**

    输入：word1 = "horse", word2 = "ros"
    输出：3
    解释：
    horse -> rorse (将 'h' 替换为 'r')
    rorse -> rose (删除 'r')
    rose -> ros (删除 'e')

**示例2**

    输入：word1 = "intention", word2 = "execution"
    输出：5
    解释：
    intention -> inention (删除 't')
    inention -> enention (将 'i' 替换为 'e')
    enention -> exention (将 'n' 替换为 'x')
    exention -> exection (将 'n' 替换为 'c')
    exection -> execution (插入 'u')

**执行结果：通过 显示详情**
太牛了，我打死也想不出来 [自底向上 和自顶向下](https://leetcode-cn.com/problems/edit-distance/solution/zi-di-xiang-shang-he-zi-ding-xiang-xia-by-powcai-3/)

- 执行用时：120 ms, 在所有 Python3 提交中击败了91.77% 的用户
内存消耗：18.6 MB, 在所有 Python3 提交中击败了15.68% 的用户
通过测试用例：1146 / 1146

```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        gao = len(word1)+1
        chang = len(word2)+1
        dp = [[0]*chang for i in range(gao)]
        word1_list = [s for s in word1]
        word1_list.insert(0, "")
        word2_list = [s for s in word2]
        word2_list.insert(0, "")

        for i in range(chang):
            dp[0][i] = i
        for i in range(gao):
            dp[i][0] = i

        for i in range(1, gao):
            for j in range(1, chang):
                if word1_list[i] == word2_list[j]:
                    dp[i][j] = dp[i-1][j-1]
                else:
                    dp[i][j] = min(dp[i-1][j-1],dp[i-1][j],dp[i][j-1]) + 1

        return dp[-1][-1]
```

**Tag: 链表、双指针、分治、排序、归并排序**

# 除法求值

Link => [除法求值](https://leetcode-cn.com/problems/evaluate-division/)

## 题目
给你一个变量对数组 equations 和一个实数值数组 values 作为已知条件，其中 equations[i] = [Ai, Bi] 和 values[i] 共同表示等式 Ai / Bi = values[i] 。每个 Ai 或 Bi 是一个表示单个变量的字符串。

另有一些以数组 queries 表示的问题，其中 queries[j] = [Cj, Dj] 表示第 j 个问题，请你根据已知条件找出 Cj / Dj = ? 的结果作为答案。

返回 所有问题的答案 。如果存在某个无法确定的答案，则用 -1.0 替代这个答案。如果问题中出现了给定的已知条件中没有出现的字符串，也需要用 -1.0 替代这个答案。

注意：输入总是有效的。你可以假设除法运算中不会出现除数为 0 的情况，且不存在任何矛盾的结果。

**示例1**
>输入：equations = [["a","b"],["b","c"]], values = [2.0,3.0], queries = [["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]<br />
>输出：[6.00000,0.50000,-1.00000,1.00000,-1.00000]<br />
>解释：条件：a / b = 2.0, b / c = 3.0<br />
>问题：a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ?<br />
>结果：[6.0, 0.5, -1.0, 1.0, -1.0 ]<br />

**示例2**
>输入：equations = [["a","b"],["b","c"],["bc","cd"]], values = [1.5,2.5,5.0], queries = [["a","c"],["c","b"],["bc","cd"],["cd","bc"]]<br />
>输出：[3.75000,0.40000,5.00000,0.20000]<br />

**执行结果：通过 显示详情**
看懵了，好难实现，还是看答案了，学习了并查集的使用，很有意思，像一颗倒着的树<br />
但是最后程度的并查集部分是自己写出来的<br />

[并查集详解](https://leetcode-cn.com/problems/number-of-provinces/solution/python-duo-tu-xiang-jie-bing-cha-ji-by-m-vjdr/)
[本题详解](https://leetcode-cn.com/problems/evaluate-division/solution/pythonbing-cha-ji-fu-mo-ban-by-milomusia-kfsu/)

- 执行用时：28 ms, 在所有 Python3 提交中击败了88.68% 的用户
内存消耗：15.1 MB, 在所有 Python3 提交中击败了35.57% 的用户
通过测试用例：24 / 24

```python
class UnionFind:
    def __init__(self):
        self.father= {}
        self.value = {}

    def add(self, x):
        if x not in self.value:
            self.father[x] = None
            self.value[x] = 1

    def find(self, x):
        root = x
        base = 1
        while self.father[root]:
            root = self.father[root]
            base *= self.value[root]
        while x != root:
            next_father = self.father[x]
            self.value[x] *= base
            base /= self.value[next_father]
            self.father[x] = root
            x = next_father
        return root
    
    def merge(self, a, b, val):
        root_a = self.find(a)
        root_b = self.find(b)
        if root_a != root_b:
            self.father[root_a] = root_b
            self.value[root_a] = self.value[b] * val / self.value[a]
    
    def is_connected(self, a, b):
        return a in self.value and b in self.value and self.find(a) == self.find(b)
            

class Solution:
    def calcEquation(self, equations: List[List[str]], values: List[float], queries: List[List[str]]) -> List[float]:
        uf = UnionFind()
        for (a,b),val in zip(equations,values):
            uf.add(a)
            uf.add(b)
            uf.merge(a,b,val)
    
        res = [-1.0] * len(queries)

        for i,(a,b) in enumerate(queries):
            if uf.is_connected(a,b):
                res[i] = uf.value[a] / uf.value[b]
        return res

```
**Tag: 深度优先搜索、广度优先搜索、并查集、图、数组、最短路**

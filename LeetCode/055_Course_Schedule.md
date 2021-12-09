# 课程表

Link => [课程表](https://leetcode-cn.com/problems/course-schedule/)

## 题目
你这个学期必须选修 numCourses 门课程，记为 0 到 numCourses - 1 。

在选修某些课程之前需要一些先修课程。 先修课程按数组 prerequisites 给出，其中 prerequisites[i] = [ai, bi] ，表示如果要学习课程 ai 则 必须 先学习课程  bi 。

    例如，先修课程对 [0, 1] 表示：想要学习课程 0 ，你需要先完成课程 1 。

请你判断是否可能完成所有课程的学习？如果可以，返回 true ；否则，返回 false 。


**示例1**
>输入：numCourses = 2, prerequisites = [[1,0]]<br />
>输出：true<br />
>解释：总共有 2 门课程。学习课程 1 之前，你需要完成课程 0 。这是可能的。<br />

**示例2**
>输入：numCourses = 2, prerequisites = [[1,0],[0,1]]<br />
>输出：false<br />
>解释：总共有 2 门课程。学习课程 1 之前，你需要先完成​课程 0 ；并且学习课程 0 之前，你还应先完成课程 1 。这是不可能的。<br />

**执行结果：通过 显示详情**
感觉重复了很多，每个都要找一遍，全部找完了通过了才算通过。。。

- 超出时间限制

```python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        if not prerequisites:
            return True

        adict = collections.defaultdict(list)
        for i in prerequisites:
            adict[i[0]].append(i[1])

        if numCourses < len(adict.keys()) + 1:
            return False

        def dfs(alist, num):
            nonlocal adict
            if adict.get(num):
                tmp = adict[num]
            else:
                return True

            for i in tmp:
                if i in alist:
                    return False

            for i in tmp:
                if not dfs(alist+[num], i):
                    return False
            return True

        for k, v in adict.items():
            alist = []
            for i in v:
                if i in alist:
                    return False

            alist.append(k)
            for i in v:
                if not dfs(alist, i):
                    return False
            continue
        else:
            return True
```
**改进：**
看了人家的文字解释，有向无环图，然后自己来写。主要还有一点就是一个点其实有三种状态，不要忘记了正在判断的状态也是不能够选择的
之前这里没有考虑到

- 执行用时：32 ms, 在所有 Python3 提交中击败了95.26% 的用户
内存消耗：17.5 MB, 在所有 Python3 提交中击败了33.15% 的用户
通过测试用例：51 / 51
```python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        if not prerequisites:
            return True

        adict = collections.defaultdict(list)
        for i in prerequisites:
            adict[i[1]].append(i[0])

        state = {}
        for k in range(numCourses):
            state[k] = 0

        def dfs(num):
            nonlocal state
            state[num] = 1
            if adict.get(num):
                for i in adict[num]:
                    if state[i] == 1:
                        return False
                    if state[i] == 2:
                        continue
                    if not dfs(i):
                        return False
            state[num] = 2
            return True

        for k, v in adict.items():
            if state[k] == 2:
                continue
            state[k] = 1
            for i in v:
                if state[k] == 2:
                    continue
                elif not dfs(i):
                    return False
            state[k] = 2
        return True
```
**Tag: 深度优先搜索、广度优先搜索、并查集、数组、矩阵**

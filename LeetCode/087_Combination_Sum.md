# 组合总和

Link => [组合总和](https://leetcode-cn.com/problems/combination-sum/)

## 题目

    给你一个 无重复元素 的整数数组 candidates 和一个目标整数 target ，找出 candidates 中可以使数字和为目标数 target 的 所有不同组合 ，并以列表形式返回。你可以按 任意顺序 返回这些组合。

    candidates 中的 同一个 数字可以 无限制重复被选取 。如果至少一个数字的被选数量不同，则两种组合是不同的。 

    对于给定的输入，保证和为 target 的不同组合数少于 150 个。

**示例1**

    输入：candidates = [2,3,6,7], target = 7
    输出：[[2,2,3],[7]]
    解释：
    2 和 3 可以形成一组候选，2 + 2 + 3 = 7 。注意 2 可以使用多次。
    7 也是一个候选， 7 = 7 。
    仅有这两种组合。

**示例2**

    输入: candidates = [2,3,5], target = 8
    输出: [[2,2,2,2],[2,3,3],[3,5]]

**执行结果：通过 显示详情**
注意不要回头就行了

- 执行用时：44 ms, 在所有 Python3 提交中击败了85.60% 的用户
内存消耗：15 MB, 在所有 Python3 提交中击败了78.36% 的用户
通过测试用例：170 / 170

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        candidates.sort()
        res_list = []
        def dfs(cur_list, tar, start):
            if tar == 0:
                res_list.append(cur_list[:])
                return
            if tar < candidates[0]:
                return
            for idx in range(start, len(candidates)):
                dfs(cur_list + [candidates[idx]], tar-candidates[idx], idx)
            
        dfs([], target, 0)
        return res_list
```

**Tag: 数组、回溯**

# 任务调度器

Link => [任务调度器](https://leetcode-cn.com/problems/task-scheduler/)

## 题目
给你一个用字符数组 tasks 表示的 CPU 需要执行的任务列表。其中每个字母表示一种不同种类的任务。任务可以以任意顺序执行，并且每个任务都可以在 1 个单位时间内执行完。在任何一个单位时间，CPU 可以完成一个任务，或者处于待命状态。

然而，两个 相同种类 的任务之间必须有长度为整数 n 的冷却时间，因此至少有连续 n 个单位时间内 CPU 在执行不同的任务，或者在待命状态。

你需要计算完成所有任务所需要的 最短时间 。

**示例1**
>输入：tasks = ["A","A","A","B","B","B"], n = 2<br />
>输出：8<br />
>解释：A -> B -> (待命) -> A -> B -> (待命) -> A -> B<br />
>在本示例中，两个相同类型任务之间必须间隔长度为 n = 2 的冷却时间，而执行一个任务只需要一个单位时间，所以中间出现了（待命）状>态。<br /> 

**示例2**
>输入：tasks = ["A","A","A","B","B","B"], n = 0<br />
>输出：6<br />
>解释：在这种情况下，任何大小为 6 的排列都可以满足要求，因为 n = 0<br />
>["A","A","A","B","B","B"]<br />
>["A","B","A","B","A","B"]<br />
>["B","B","B","A","A","A"]<br />
>...<br />
>诸如此类<br />

执行结果：
通过
显示详情

添加备注
执行用时：3380 ms, 在所有 Python3 提交中击败了5.07% 的用户
内存消耗：16.7 MB, 在所有 Python3 提交中击败了31.77% 的用户
通过测试用例：71 / 71

```python
class Solution:
    def leastInterval(self, tasks: List[str], n: int) -> int:
        count_dict = {}
        count_list = []
        count_time = {}
        time_do = 0

        for task in tasks:
            if task in count_dict:
                count_dict[task] += 1
            else:
                count_dict[task] = 1

        for k, v in count_dict.items():
            count_list.append([k, v])
            count_time[k] = 0

        while count_list:
            # 按个数排序
            count_list.sort(key=lambda x:x[1], reverse = True)

            for index in range(len(count_list)):
                # 判断是不是冷却
                if count_time[count_list[index][0]] == 0:
                    # 选他
                    time_do += 1
                    # 定时器记录
                    count_time[count_list[index][0]] = n
                    # 总量-1
                    count_list[index][1] -= 1
                    # 刷新计时器
                    for k, v in count_time.items():
                        if v != 0 and k != count_list[index][0]:
                            count_time[k] -= 1
                    # 判断是否没了, 没了要清除, 还要在计时器里清除
                    if count_list[index][1] == 0:
                        count_time.pop(count_list[index][0])
                        count_list.pop(index)
                    break
            else:
                time_do += 1
                for k, v in count_time.items():
                    if v != 0:
                        count_time[k] -= 1
        return time_do
                
```
改进：
执行结果：
通过
显示详情

添加备注
执行用时：68 ms, 在所有 Python3 提交中击败了69.40% 的用户
内存消耗：16.5 MB, 在所有 Python3 提交中击败了87.74% 的用户
通过测试用例：71 / 71

居然是先放好，再想，我想不到哇，我想的是一个一个放，怎么样放的策略

```python
class Solution(object):
    def leastInterval(self, tasks, n):
        length = len(tasks)
        if length <= 1:
            return length
        
        # 用于记录每个任务出现的次数
        task_map = dict()
        for task in tasks:
            task_map[task] = task_map.get(task, 0) + 1
        # 按任务出现的次数从大到小排序
        task_sort = sorted(task_map.items(), key=lambda x: x[1], reverse=True)
        
        # 出现最多次任务的次数
        max_task_count = task_sort[0][1]
        # 至少需要的最短时间
        res = (max_task_count - 1) * (n + 1)
        
        for sort in task_sort:
            if sort[1] == max_task_count:
                res += 1
        
        # 如果结果比任务数量少，则返回总任务数
        return res if res >= length else length
```
**Tag: 贪心、数组、哈希表、计数、排序、堆（优先队列）**

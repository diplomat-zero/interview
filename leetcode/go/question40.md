```
给定一个候选人编号的集合 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的每个数字在每个组合中只能使用 一次 。

注意：解集不能包含重复的组合。 

 

示例 1:

输入: candidates = [10,1,2,7,6,1,5], target = 8,
输出:
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
示例 2:

输入: candidates = [2,5,2,1,2], target = 5,
输出:
[
[1,2,2],
[5]
]
 

提示:

1 <= candidates.length <= 100
1 <= candidates[i] <= 50
1 <= target <= 30
```

```

```

```
func combinationSum2(candidates []int, target int) [][]int {
    sort.Ints(candidates)
    res = make([][]int, 0)
    trace := make([]int, 0)
    dfs(candidates, target, 0, trace)
    return res
}
var res [][]int

func dfs(candidates []int, target int, start int, trace []int) {
    if target == 0 {
        tmp := make([]int, len(trace))
        copy(tmp, trace)
        res = append(res, tmp)
        return
    }

    for i := start; i < len(candidates); i++ {
        if candidates[i] > target {
            continue
        }
        if i > start && candidates[i] == candidates[i - 1] {
            continue
        }

        trace = append(trace, candidates[i])
        dfs(candidates, target - candidates[i], i + 1, trace)
        trace = trace[:len(trace) - 1]
    }
}
```
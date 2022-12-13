```
给你一个整数数组 nums ，其中可能包含重复元素，请你返回该数组所有可能的子集（幂集）。

解集 不能 包含重复的子集。返回的解集中，子集可以按 任意顺序 排列。

 

示例 1：

输入：nums = [1,2,2]
输出：[[],[1],[1,2],[1,2,2],[2],[2,2]]
示例 2：

输入：nums = [0]
输出：[[],[0]]
 

提示：

1 <= nums.length <= 10
-10 <= nums[i] <= 10
```

```

```

```
func subsetsWithDup(nums []int) [][]int {
    res = make([][]int, 0)
    trace := make([]int, 0)
    sort.Ints(nums)
    dfs(nums, trace, 0)
    return res
}
var res [][]int
func dfs(nums []int, trace []int, start int) {
    temp := make([]int, len(trace))
    copy(temp, trace)
    res = append(res, temp)
    
    for i := start; i < len(nums); i++ {
        if i > start && nums[i] == nums[i - 1] {
            continue
        }
        trace = append(trace, nums[i])
        dfs(nums, trace, i + 1)
        trace = trace[:len(trace) - 1]
    }
}
```
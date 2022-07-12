```
给你一个整数数组 nums ，数组中的元素 互不相同 。返回该数组所有可能的子集（幂集）。

解集 不能 包含重复的子集。你可以按 任意顺序 返回解集。

 

示例 1：

输入：nums = [1,2,3]
输出：[[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
示例 2：

输入：nums = [0]
输出：[[],[0]]
 

提示：

1 <= nums.length <= 10
-10 <= nums[i] <= 10
nums 中的所有元素 互不相同
```

```

```

```
func subsets(nums []int) [][]int {
    trace := make([]int, 0)
    res = make([][]int, 0)
    dfs(nums, trace, 0)
    return res
}

var res [][]int
func dfs(nums []int, trace []int, start int) {
    cp := make([]int, len(trace))
    copy(cp, trace)
    res = append(res, cp)
    for i := start; i < len(nums); i++ {
        trace = append(trace, nums[i])
        dfs(nums, trace, i + 1)
        trace = trace[:len(trace) - 1]
    }
}
```
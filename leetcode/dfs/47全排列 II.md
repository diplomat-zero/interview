```
给定一个可包含重复数字的序列 nums ，按任意顺序 返回所有不重复的全排列。

 

示例 1：

输入：nums = [1,1,2]
输出：
[[1,1,2],
 [1,2,1],
 [2,1,1]]
示例 2：

输入：nums = [1,2,3]
输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
 

提示：

1 <= nums.length <= 8
-10 <= nums[i] <= 10
```

```

```

```
func permuteUnique(nums []int) [][]int {
    sort.Ints(nums)
    res = make([][]int, 0)
    trace := make([]int, 0)
    visited := make([]bool, len(nums))
    dfs(nums, trace, visited)
    return res
}

var res [][]int

func dfs(nums []int, trace []int, visited []bool) {
    if len(trace) == len(nums) {
        temp := make([]int, len(trace))
        copy(temp, trace)
        res = append(res, temp)
        return
    }

    for i := 0; i < len(nums); i++ {
        if visited[i] {
            continue
        }

        if i > 0 && nums[i] == nums[i - 1] && !visited[i - 1] {
            continue
        }

        trace = append(trace, nums[i])
        visited[i] = true
        dfs(nums, trace, visited)
        trace = trace[:len(trace) - 1]
        visited[i] = false
    }
}
```
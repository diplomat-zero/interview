```
给定一个不含重复数字的数组 nums ，返回其 所有可能的全排列 。你可以 按任意顺序 返回答案。

 

示例 1：

输入：nums = [1,2,3]
输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
示例 2：

输入：nums = [0,1]
输出：[[0,1],[1,0]]
示例 3：

输入：nums = [1]
输出：[[1]]
 

提示：

1 <= nums.length <= 6
-10 <= nums[i] <= 10
nums 中的所有整数 互不相同
```

```

```

```
func permute(nums []int) [][]int {
    trace := make([]int, 0)
    flags := make([]bool, len(nums))
    res := make([][]int, 0)

    var dfs func()
    dfs = func() {
        if len(trace) == len(nums) {
            temp := make([]int, len(trace))
            copy(temp, trace)
            res = append(res, temp)
            return
        }

        for i := range nums {
            if flags[i] {
                continue
            }
            flags[i] = true
            trace = append(trace, nums[i])
            dfs()
            flags[i] = false
            trace = trace[:len(trace) - 1]
        }
    }

    dfs()
    return res
}
```
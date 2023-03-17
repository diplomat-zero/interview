```
给定一个二进制数组 nums , 找到含有相同数量的 0 和 1 的最长连续子数组，并返回该子数组的长度。

 

示例 1:

输入: nums = [0,1]
输出: 2
说明: [0, 1] 是具有相同数量 0 和 1 的最长连续子数组。
示例 2:

输入: nums = [0,1,0]
输出: 2
说明: [0, 1] (或 [1, 0]) 是具有相同数量0和1的最长连续子数组。
 

提示：

1 <= nums.length <= 105
nums[i] 不是 0 就是 1
```

```

```

```
func findMaxLength(nums []int) int {
    for key,value := range nums {
        if value == 0 {
            nums[key] = -1
        }
    } 
    pre_sum := make([]int, len(nums) + 1)
    pre_sum[0] = 0
    for i := 0; i < len(nums); i++ {
        pre_sum[i + 1] = pre_sum[i] + nums[i]
    }

    hash_map := make(map[int]int)
    for m := 0; m < len(pre_sum); m++ {
        if _,ok := hash_map[pre_sum[m]]; !ok {
            hash_map[pre_sum[m]] = m
        }
    }
    res := 0
    for n := 1; n < len(pre_sum); n++ {
        if _,ok := hash_map[pre_sum[n]]; ok {
            if n - hash_map[pre_sum[n]] > res {
                res = n - hash_map[pre_sum[n]]
            }
        }
    }
    return res
}
```
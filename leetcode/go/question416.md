```
给你一个 只包含正整数 的 非空 数组 nums 。请你判断是否可以将这个数组分割成两个子集，使得两个子集的元素和相等。

 

示例 1：

输入：nums = [1,5,11,5]
输出：true
解释：数组可以分割成 [1, 5, 5] 和 [11] 。
示例 2：

输入：nums = [1,2,3,5]
输出：false
解释：数组不能分割成两个元素和相等的子集。
 

提示：

1 <= nums.length <= 200
1 <= nums[i] <= 100
```

```

```

```
func canPartition(nums []int) bool {
    sort.Ints(nums)
    sum := 0
    for _,value := range nums {
        sum += value
    }
    if sum % 2 != 0 {
        return false
    }
    need_sum := sum / 2
    dp := make([][]bool, len(nums) + 1)
    for i := 0; i < len(dp); i++ {
        dp[i] = make([]bool, need_sum + 1)
        dp[i][0] = true
    }
    for i := 1; i <= len(nums); i++ {
        for j := 1; j <= need_sum; j++ {
            if nums[i - 1] > j {
                dp[i][j] = dp[i - 1][j]
            } else {
                dp[i][j] = dp[i - 1][j] || dp[i - 1][j - nums[i - 1]]
            }
        }
    }
    return dp[len(nums)][need_sum]
}
```
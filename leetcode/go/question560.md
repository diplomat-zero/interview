```
给你一个整数数组 nums 和一个整数 k ，请你统计并返回 该数组中和为 k 的连续子数组的个数 。

 

示例 1：

输入：nums = [1,1,1], k = 2
输出：2
示例 2：

输入：nums = [1,2,3], k = 3
输出：2
 

提示：

1 <= nums.length <= 2 * 104
-1000 <= nums[i] <= 1000
-107 <= k <= 107
```

```

```

```
func subarraySum(nums []int, k int) int {
    hash := make(map[int]int)
    pre_sum := make([]int, len(nums) + 1)
    res := 0
    pre_sum[0] = 0
    hash[0] = 1
    for i := 1; i <= len(nums); i++ {
        pre_sum[i] = pre_sum[i - 1] + nums[i - 1]
        need := pre_sum[i] - k
        if value,ok := hash[need]; ok {
            res += value
        }

        if _,ok := hash[pre_sum[i]]; ok {
            hash[pre_sum[i]]++
        } else {
            hash[pre_sum[i]] = 1
        }

    }
    return res
}
```
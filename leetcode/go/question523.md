```
给你一个整数数组 nums 和一个整数 k ，编写一个函数来判断该数组是否含有同时满足下述条件的连续子数组：

子数组大小 至少为 2 ，且
子数组元素总和为 k 的倍数。
如果存在，返回 true ；否则，返回 false 。

如果存在一个整数 n ，令整数 x 符合 x = n * k ，则称 x 是 k 的一个倍数。0 始终视为 k 的一个倍数。

 

示例 1：

输入：nums = [23,2,4,6,7], k = 6
输出：true
解释：[2,4] 是一个大小为 2 的子数组，并且和为 6 。
示例 2：

输入：nums = [23,2,6,4,7], k = 6
输出：true
解释：[23, 2, 6, 4, 7] 是大小为 5 的子数组，并且和为 42 。 
42 是 6 的倍数，因为 42 = 7 * 6 且 7 是一个整数。
示例 3：

输入：nums = [23,2,6,4,7], k = 13
输出：false
 

提示：

1 <= nums.length <= 105
0 <= nums[i] <= 109
0 <= sum(nums[i]) <= 231 - 1
1 <= k <= 231 - 1
```

```

```

```
func checkSubarraySum(nums []int, k int) bool {
    pre_sum := make([]int, len(nums) + 1)
    pre_sum[0] = 0
    for i := 0; i < len(nums); i++ {
        pre_sum[i + 1] = pre_sum[i] + nums[i]
    }
    hash_map := make(map[int]int)
    for m := 0; m < len(pre_sum); m++ {
        val := pre_sum[m] % k
        if _,ok := hash_map[val]; !ok {
            hash_map[val] = m
        }
    }
    for n := 1; n < len(pre_sum); n++ {
        val1 := pre_sum[n] % k
        if _,ok := hash_map[val1]; ok {
            if n - hash_map[val1] >= 2 {
                return true
            }
        }
    }
    return false
}
```
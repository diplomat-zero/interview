```
给你一个整型数组 nums ，在数组中找出由三个数组成的最大乘积，并输出这个乘积。

 

示例 1：

输入：nums = [1,2,3]
输出：6
示例 2：

输入：nums = [1,2,3,4]
输出：24
示例 3：

输入：nums = [-1,-2,-3]
输出：-6
 

提示：

3 <= nums.length <= 104
-1000 <= nums[i] <= 1000
```

```

```

```
func maximumProduct(nums []int) int {
    min_fu_1 := math.MaxInt64
    min_fu_2 := math.MaxInt64
    max_zheng_1 := math.MinInt64
    max_zheng_2 := math.MinInt64
    max_zheng_3 := math.MinInt64
    for i := 0; i < len(nums); i++ {
        if nums[i] > max_zheng_1 {
            max_zheng_3 = max_zheng_2
            max_zheng_2 = max_zheng_1
            max_zheng_1 = nums[i]
        } else if nums[i] > max_zheng_2 {
            max_zheng_3 = max_zheng_2
            max_zheng_2 = nums[i]
        } else if nums[i] > max_zheng_3 {
            max_zheng_3 = nums[i]
        }
        if nums[i] < min_fu_1 {
            min_fu_2 = min_fu_1
            min_fu_1 = nums[i]
        } else if nums[i] < min_fu_2 {
            min_fu_2 = nums[i]
        }
    }

    if max_zheng_1 * max_zheng_2 * max_zheng_3 > max_zheng_1 * min_fu_1 * min_fu_2 {
        return max_zheng_1 * max_zheng_2 * max_zheng_3
    } else {
        return max_zheng_1 * min_fu_1 * min_fu_2
    }
}
```
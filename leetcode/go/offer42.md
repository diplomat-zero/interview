```
输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。
要求时间复杂度为O(n)。

示例1:
输入: nums = [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
 
提示：
1 <= arr.length <= 10^5
-100 <= arr[i] <= 100
```

```
func maxSubArray(nums []int) int {
    max := nums[0]
    sum := nums[0]

    for i := 1; i < len(nums); i++ {
        if sum > 0 {
            sum += nums[i]
        } else {
            sum = nums[i]
        }

        max = maxnum(max, sum)
    }

    return max
}

func maxnum(x, y int) int {
    if x > y {
        return x
    }
    return y
}
```
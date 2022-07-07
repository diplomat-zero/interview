```
统计一个数字在排序数组中出现的次数。

 

示例 1:

输入: nums = [5,7,7,8,8,10], target = 8
输出: 2
示例 2:

输入: nums = [5,7,7,8,8,10], target = 6
输出: 0
 

提示：

0 <= nums.length <= 105
-109 <= nums[i] <= 109
nums 是一个非递减数组
-109 <= target <= 109
```

```

```

```
func search(nums []int, target int) int {
    left := 0
    right := len(nums) - 1
    for left <= right {
        mid := (right - left) / 2 + left
        if nums[mid] == target {
            start := mid
            end := mid
            for start >= left && nums[start] == target  {
                start--
            }
            for end <= right && nums[end] == target  {
                end++
            }
            return end - start - 1
        } else if nums[mid] > target {
            right = mid - 1
        } else {
            left = mid + 1
        }
    }
    return 0
}
```
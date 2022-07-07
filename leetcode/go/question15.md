```
给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有和为 0 且不重复的三元组。

注意：答案中不可以包含重复的三元组。

 

示例 1：

输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]
示例 2：

输入：nums = []
输出：[]
示例 3：

输入：nums = [0]
输出：[]
 

提示：

0 <= nums.length <= 3000
-105 <= nums[i] <= 105
```

```

```

```
func threeSum(nums []int) [][]int {
    nums1 := nums[:]
    sort.Ints(nums1)
    res := make([][]int, 0)
    for i := 0; i < len(nums1); i++ {
        if i > 0 && nums1[i] == nums1[i - 1] {
            continue
        }
        left := i + 1
        right := len(nums1) - 1
        for left < right {
            sum := nums1[i] + nums1[left] + nums1[right]
            if sum == 0 {
                res = append(res, []int{nums[i], nums[left], nums[right]})
                for left < right && nums1[left] == nums1[left + 1] {
                    left++
                }
                left++
                for left < right && nums1[right] == nums1[right - 1] {
                    right--
                }
                right--
            } else if sum > 0 {
                right--
            } else {
                left++
            }
        }
    }
    return res
}
```
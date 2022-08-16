```
给你一个正整数 n ，请你找出符合条件的最小整数，其由重新排列 n 中存在的每位数字组成，并且其值大于 n 。如果不存在这样的正整数，则返回 -1 。

注意 ，返回的整数应当是一个 32 位整数 ，如果存在满足题意的答案，但不是 32 位整数 ，同样返回 -1 。

 

示例 1：

输入：n = 12
输出：21
示例 2：

输入：n = 21
输出：-1
 

提示：

1 <= n <= 231 - 1
```

```

```

```
func nextGreaterElement(n int) int {
    nums := []byte(strconv.Itoa(n))
    i := len(nums) - 2
    j := len(nums) - 1
    for i >= 0 && nums[i] >= nums[j] {
        i--
        j--
    }
    if i < 0 {
        return -1
    }
    k := len(nums) - 1
    for nums[k] <= nums[i] {
        k--
    }

    nums[k], nums[i] = nums[i],nums[k]

    left := i + 1
    right := len(nums) - 1
    for left < right {
        nums[left], nums[right] = nums[right], nums[left]
        left++
        right--
    }
    ans, _ := strconv.Atoi(string(nums))
    if ans > math.MaxInt32 {
        return -1
    }
    return ans
}
```
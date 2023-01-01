```
给你一个整数数组 nums ，你需要找出一个 连续子数组 ，如果对这个子数组进行升序排序，那么整个数组都会变为升序排序。

请你找出符合题意的 最短 子数组，并输出它的长度。

 

示例 1：

输入：nums = [2,6,4,8,10,9,15]
输出：5
解释：你只需要对 [6, 4, 8, 10, 9] 进行升序排序，那么整个表都会变为升序排序。
示例 2：

输入：nums = [1,2,3,4]
输出：0
示例 3：

输入：nums = [1]
输出：0
 

提示：

1 <= nums.length <= 104
-105 <= nums[i] <= 105
 

进阶：你可以设计一个时间复杂度为 O(n) 的解决方案吗？
```

```
按题意，这个最短无序子数组可以把整个数组可以分成三个部分，第一部分是有序的，第二部分是答案，也就是无序子数组，第三部分仍然是有序的。

比如示例1，第1部分为[2]，第二部分（也就是答案)是[6,4,8,10,9]，第3部分是[15]。

如果能找到边界，那么就能划分出这三个部分了。左边界left，一定能是[left]>[left+1]，而右边一定满足[right−1]>[right]。因为对于有序的话，一定都是[i]<[i+1]的。

可以分别查找left，而且注意当left到达n−1时，说明数组是升序的；同理查找right时如果right到达0时，说明也是升序的。

这样，left会指向左边第一个乱序的元素，right指向右边第一个乱序，right−left+1即是个数。

但还要注意，要想把第二部分排序后整体是升序，那么第二部分的所有元素要大于等于第一部分，同时要小于等于第三部分，这是一个很重要的隐含条件。

因此，需要找到[left,right]之间的最大值和最小值，如果[left−1]大于min，就需要向左扩；如果[right+1]小于最大值，就需要向右扩。

时间复杂度是O(n)，最多遍历三遍数组。
```

```
func findUnsortedSubarray(nums []int) int {
    left := 0
    right := len(nums) - 1
    for left < right {
        if nums[left] > nums[left + 1] {
            break
        }
        left++
    }
    if left == len(nums) - 1 {
        return 0
    }
    for left < right {
        if nums[right] < nums[right - 1] {
            break
        }
        right--
    }
    if right == 0 {
        return 0
    }
    min := math.MaxInt64
    max := math.MinInt64
    for i := left; i <= right; i++ {
        if nums[i] < min {
            min = nums[i]
        }
        if nums[i] > max {
            max = nums[i]
        }
    }
    for left > 0 && nums[left - 1] > min {
        left--
    }
    for right < len(nums) - 1 && nums[right + 1] < max {
        right++
    }
    return right - left + 1
}
```
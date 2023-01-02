```
给你一个整数数组 nums，请你将该数组升序排列。

 

示例 1：

输入：nums = [5,2,3,1]
输出：[1,2,3,5]
示例 2：

输入：nums = [5,1,1,2,0,0]
输出：[0,0,1,1,2,5]
 

提示：

1 <= nums.length <= 5 * 104
-5 * 104 <= nums[i] <= 5 * 104
```

```

```

```
func sortArray(nums []int) []int {
    quickSort(nums, 0, len(nums) - 1)
    return nums
}

func quickSort(nums []int, left int, right int) {
    if left < right {
        find := findNum(nums, left, right)
        quickSort(nums, left, find - 1)
        quickSort(nums, find + 1, right)
    }
}

func findNum(nums []int, left int, right int) int {
    target := nums[left]
    for left < right {
        for left < right && nums[right] >= target {
            right--
        }
        nums[left], nums[right] = nums[right], nums[left]
        for left < right && nums[left] <= target {
            left++
        }
        nums[left], nums[right] = nums[right], nums[left]
    }
    return left
}
```

```
func reversePairs(nums []int) int {
	return splitNums(nums)
}

func splitNums(nums []int) []int {
	if len(nums) <= 1 {
		return nums
	}
	mid := len(nums) / 2
	nums1 := splitNums(nums[:mid])
	nums2 := splitNums(nums[mid:])
	return mergeNums(nums1, nums2)
}

func mergeNums(nums1 []int, nums2 []int) []int {
	i := 0
	j := 0
	res := make([]int, 0)
	for i < len(nums1) && j < len(nums2) {
		if nums1[i] < nums2[j] {
			res = append(res, nums1[i])
			i++
		} else {
			res = append(res, nums2[j])
			j++
		}
	}
	for i < len(nums1) {
		res = append(res, nums1[i])
		i++
	}
	for j < len(nums2) {
		res = append(res, nums2[j])
		j++
	}
	return res
}
```
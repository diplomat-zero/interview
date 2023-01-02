```
在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

 

示例 1:

输入: [7,5,6,4]
输出: 5
 

限制：

0 <= 数组长度 <= 50000
```

```

```

```
func reversePairs(nums []int) int {
    result = 0
	splitNums(nums)
	return result
}

var result int

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
		if nums1[i] <= nums2[j] {
			res = append(res, nums1[i])
			i++
		} else {
			result += len(nums1) - i
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
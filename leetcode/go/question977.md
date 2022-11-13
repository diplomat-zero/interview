```

```

```

```

```
func sortedSquares(nums []int) []int {
    fu := make([]int, 0)
	zheng := make([]int, 0)
	for i := 0; i < len(nums); i++ {
		if nums[i] < 0 {
			fu = append([]int{nums[i] * nums[i]}, fu...)
		} else {
			zheng = append(zheng, nums[i]*nums[i])
		}
	}
	i := 0
	j := 0
	res := make([]int, 0)
	for i < len(fu) && j < len(zheng) {
		if fu[i] > zheng[j] {
			res = append(res, zheng[j])
			j++
		} else {
			res = append(res, fu[i])
			i++
		}
	}
	for i < len(fu) {
		res = append(res, fu[i])
		i++
	}
	for j < len(zheng) {
		res = append(res, zheng[j])
		j++
	}
	return res
}
```
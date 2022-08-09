```
给定一组非负整数 nums，重新排列每个数的顺序（每个数不可拆分）使之组成一个最大的整数。

注意：输出结果可能非常大，所以你需要返回一个字符串而不是整数。

 

示例 1：

输入：nums = [10,2]
输出："210"
示例 2：

输入：nums = [3,30,34,5,9]
输出："9534330"
 

提示：

1 <= nums.length <= 100
0 <= nums[i] <= 109
```

```

```

```
func largestNumber(nums []int) string {
    for i := 0; i < len(nums); i++ {
		for j := i + 1; j < len(nums); j++ {
			first := strconv.Itoa(nums[i])
			second := strconv.Itoa(nums[j])
			num1, _ := strconv.Atoi(first + second)
			num2, _ := strconv.Atoi(second + first)
			if num1 < num2 {
				nums[i], nums[j] = nums[j], nums[i]
			}
		}
	}
    if nums[0] == 0 {
        return "0"
    }
	res := ""
	for i := 0; i < len(nums); i++ {
		res += strconv.Itoa(nums[i])
	}
	return res
}
```
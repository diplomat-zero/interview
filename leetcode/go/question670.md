```
给定一个非负整数，你至多可以交换一次数字中的任意两位。返回你能得到的最大值。

示例 1 :

输入: 2736
输出: 7236
解释: 交换数字2和数字7。
示例 2 :

输入: 9973
输出: 9973
解释: 不需要交换。
注意:

给定数字的范围是 [0, 108]
```

```

```

```
func maximumSwap(num int) int {
    m_str := strconv.Itoa(num)
	cur := make([]int, 0)
	max := make([]int, 0)
	for i := 0; i < len(m_str); i++ {
		n, _ := strconv.Atoi(string(m_str[i]))
		cur = append(cur, n)
		max = append(max, n)
	}
	sort.Ints(max)
	left := 0
	right := len(max) - 1
	for left < right {
		max[left], max[right] = max[right], max[left]
		left++
		right--
	}
	i := 0
	find := 0
	for i < len(cur) {
		if cur[i] != max[i] {
			find = max[i]
			break
		}
		i++
	}
	if i == len(cur) {
		res := 0
		n := 0
		for m := len(cur) - 1; m >= 0; m-- {
			res += cur[m] * int(math.Pow10(n))
			n++
		}
		return res
	}
	swap := 0
	for j := len(cur) - 1; j >= 0; j-- {
		if cur[j] == find {
			swap = j
			break
		}
	}
	cur[swap], cur[i] = cur[i], cur[swap]
	res := 0
	n := 0
	for m := len(cur) - 1; m >= 0; m-- {
		res += cur[m] * int(math.Pow10(n))
		n++
	}
	return res

}
```
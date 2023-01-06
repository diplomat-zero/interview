```
给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。

 

示例 1:



输入：heights = [2,1,5,6,2,3]
输出：10
解释：最大的矩形为图中红色区域，面积为 10
示例 2：



输入： heights = [2,4]
输出： 4
 

提示：

1 <= heights.length <=105
0 <= heights[i] <= 104
```

```

```

```
func largestRectangleArea(heights []int) int {
    new_heights := make([]int, 0)
	new_heights = append(new_heights, 0)
	for i := 1; i <= len(heights); i++ {
		new_heights = append(new_heights, heights[i-1])
	}
	new_heights = append(new_heights, 0)
	stack := make([]int, 0)
	res := 0
	for i := 0; i < len(new_heights); i++ {
		for len(stack) > 0 && new_heights[i] < new_heights[stack[len(stack)-1]] {
			high := new_heights[stack[len(stack)-1]]
			stack = stack[:len(stack)-1]
			right := i
			left := stack[len(stack)-1]
			area := high * (right - left - 1)
			if area > res {
				res = area
			}
		}
		stack = append(stack, i)
	}
	return res
}
```
```
给你一个大小为 m x n 的矩阵 mat ，请以对角线遍历的顺序，用一个数组返回这个矩阵中的所有元素。

 

示例 1：


输入：mat = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,4,7,5,3,6,8,9]
示例 2：

输入：mat = [[1,2],[3,4]]
输出：[1,2,3,4]
 

提示：

m == mat.length
n == mat[i].length
1 <= m, n <= 104
1 <= m * n <= 104
-105 <= mat[i][j] <= 105
```

```

```

```
func findDiagonalOrder(mat [][]int) []int {
    result := make(map[int][]int)
    for i := 0; i < len(mat); i++ {
		for j := 0; j < len(mat[0]); j++ {
			tmp := make([]int, 0)
			if _, ok := result[i+j]; ok {
				tmp = result[i+j]
			}
			tmp = append(tmp, mat[i][j])
			result[i+j] = tmp
		}
	}

    res := make([]int, 0)
	for m := 0; m < len(result); m++ {
		tmp := result[m]
		if m % 2 == 0 {
			for p := len(tmp) - 1; p >= 0; p-- {
				res = append(res, tmp[p])
			}
		} else {
			for q := 0; q < len(tmp); q++ {
				res = append(res, tmp[q])
			}
		}
	}
    return res
}
```
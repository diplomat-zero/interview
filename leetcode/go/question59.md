```
给你一个正整数 n ，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的 n x n 正方形矩阵 matrix 。

 

示例 1：


输入：n = 3
输出：[[1,2,3],[8,9,4],[7,6,5]]
示例 2：

输入：n = 1
输出：[[1]]
 

提示：

1 <= n <= 20
```

```

```

```
func generateMatrix(n int) [][]int {
    res := make([][]int, n)
    for i := 0; i < len(res); i++ {
        res[i] = make([]int, n)
    }
    total := n * n
    left := 0
    right := n - 1
    top := 0
    bottom := n - 1
    num := 1
    for total >= 1 {
        for i := left; i <= right && total >= 1; i++ {
            res[top][i] = num
            num++
            total--
        }
        top++

        for i := top; i <= bottom && total >= 1; i++ {
            res[i][right] = num
            total--
            num++
        }
        right--

        for i := right; i >= left && total >= 1; i-- {
            res[bottom][i] = num
            total--
            num++
        }
        bottom--

        for i := bottom; i >= top && total >= 1; i-- {
            res[i][left] = num
            total--
            num++
        }
        left++
    }
    return res
}
```
```
输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

示例 1：
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]

示例 2：
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
 
限制：
0 <= matrix.length <= 100
0 <= matrix[i].length <= 100
```

```
func spiralOrder(matrix [][]int) []int {
    if len(matrix) == 0 || len(matrix[0]) == 0 {
        return nil
    }

    top := 0
    bottom := len(matrix) - 1

    left := 0
    right := len(matrix[0]) - 1

    total := len(matrix) * len(matrix[0])

    ret := []int{}

    for total > 0 {
        for i := left; i <= right && total > 0; i++ {
            ret = append(ret, matrix[top][i])
            total--
        } 
        top++

        for i := top; i <= bottom && total > 0; i++ {
            ret = append(ret, matrix[i][right])
            total--
        }
        right--

        for i := right; i >= left && total > 0; i-- {
            ret = append(ret, matrix[bottom][i])
            total--
        }
        bottom--

        for i := bottom; i >= top && total > 0; i-- {
            ret = append(ret, matrix[i][left])
            total--
        }
        left++
    }

    return ret
}
```
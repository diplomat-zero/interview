```
在一个由 '0' 和 '1' 组成的二维矩阵内，找到只包含 '1' 的最大正方形，并返回其面积。

 

示例 1：


输入：matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
输出：4
示例 2：


输入：matrix = [["0","1"],["1","0"]]
输出：1
示例 3：

输入：matrix = [["0"]]
输出：0
 

提示：

m == matrix.length
n == matrix[i].length
1 <= m, n <= 300
matrix[i][j] 为 '0' 或 '1'
```

```

```

```
func maximalSquare(matrix [][]byte) int {
    dp := make([][]int, len(matrix))
    for m := 0; m < len(dp); m++ {
        dp[m] = make([]int, len(matrix[0]))
    }
    for i := 0; i < len(matrix); i++ {
        if matrix[i][0] == '0' {
            dp[i][0] = 0
        } else {
            dp[i][0] = 1
        }
    }
    for j := 0; j < len(matrix[0]); j++ {
        if matrix[0][j] == '0' {
            dp[0][j] = 0
        } else {
            dp[0][j] = 1
        }
    }

    res := math.MinInt
    for p := 1; p < len(matrix); p++ {
        for q := 1; q < len(matrix[0]); q++ {
            if matrix[p][q] == '0' {
                dp[p][q] = 0 
            } else {
                if dp[p][q - 1] < dp[p - 1][q] {
                    dp[p][q] = dp[p][q - 1]
                } else {
                    dp[p][q] = dp[p - 1][q]
                }
                if dp[p][q] > dp[p - 1][q - 1] {
                    dp[p][q] = dp[p - 1][q - 1]
                }
                dp[p][q] = dp[p][q] + 1
            }
        } 
    }

    for a := 0; a < len(dp); a++ {
        for b := 0; b < len(dp[0]); b++ {
            if dp[a][b] > res {
                res = dp[a][b]
            }
        }
    }

    return res * res
}
```
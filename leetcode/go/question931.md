```
给你一个 n x n 的 方形 整数数组 matrix ，请你找出并返回通过 matrix 的下降路径 的 最小和 。

下降路径 可以从第一行中的任何元素开始，并从每一行中选择一个元素。在下一行选择的元素和当前行所选元素最多相隔一列（即位于正下方或者沿对角线向左或者向右的第一个元素）。具体来说，位置 (row, col) 的下一个元素应当是 (row + 1, col - 1)、(row + 1, col) 或者 (row + 1, col + 1) 。

 

示例 1：



输入：matrix = [[2,1,3],[6,5,4],[7,8,9]]
输出：13
解释：如图所示，为和最小的两条下降路径
示例 2：



输入：matrix = [[-19,57],[-40,-5]]
输出：-59
解释：如图所示，为和最小的下降路径
 

提示：

n == matrix.length == matrix[i].length
1 <= n <= 100
-100 <= matrix[i][j] <= 100
```

```

```

```
func minFallingPathSum(matrix [][]int) int {
    dp := make([][]int, len(matrix))
    for i := 0; i < len(dp); i++ {
        dp[i] = make([]int, len(matrix))
    }
    for i := 0; i < len(matrix); i++ {
        dp[0][i] = matrix[0][i]
    }
    for i := 1; i < len(matrix); i++ {
        for j := 0; j < len(matrix); j++ {
            if j == 0 {
                dp[i][j] = min(dp[i - 1][j], dp[i - 1][j + 1]) + matrix[i][j]
            } else if j == len(matrix) - 1 {
                dp[i][j] = min(dp[i - 1][j], dp[i - 1][j - 1]) + matrix[i][j]
            } else {
                dp[i][j] = min(dp[i - 1][j], min(dp[i - 1][j - 1], dp[i - 1][j + 1])) + matrix[i][j]
            }
        }
    }
    res := math.MaxInt64
    for i := 0; i < len(matrix); i++ {
        res = min(res, dp[len(matrix) - 1][i])
    }
    return res
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}
```
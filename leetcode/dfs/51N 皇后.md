```
按照国际象棋的规则，皇后可以攻击与之处在同一行或同一列或同一斜线上的棋子。

n 皇后问题 研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。

给你一个整数 n ，返回所有不同的 n 皇后问题 的解决方案。

每一种解法包含一个不同的 n 皇后问题 的棋子放置方案，该方案中 'Q' 和 '.' 分别代表了皇后和空位。

 

示例 1：


输入：n = 4
输出：[[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
解释：如上图所示，4 皇后问题存在两个不同的解法。
示例 2：

输入：n = 1
输出：[["Q"]]
 

提示：

1 <= n <= 9
```

```

```

```
func solveNQueens(n int) [][]string {
    board := make([][]string, n)
    for i := 0; i < len(board); i++ {
        board[i] = make([]string, n)
    }
    for i := 0; i < n; i++ {
        for j := 0; j < n; j++ {
            board[i][j] = "."
        }
    }
    res = make([][]string, 0)
    dfs(board, 0)
    return res
}
var res [][]string
func dfs(board [][]string, row int) {
    if row == len(board) {
        result := make([]string, 0)
        for i := 0; i < len(board); i++ {
            tmp := ""
            for j := 0; j < len(board[0]); j++ {
                tmp += board[i][j]
            }
            result = append(result, tmp)
        }
        res = append(res, result)
        return
    }

    for i := 0; i < len(board[row]); i++ {
        if (valid(board, row, i)) {
            board[row][i] = "Q"
            dfs(board, row + 1)
            board[row][i] = "."
        }
    }
}

func valid(board [][]string, row int, col int) bool {
    for i := 0; i < len(board); i++ {
        if board[row][i] == "Q" {
            return false
        }
        if board[i][col] == "Q" {
            return false
        }
    }
    i, j := row - 1, col - 1
    for i >= 0 && j >= 0 {
        if board[i][j] == "Q" {
            return false
        }
        i--
        j--
    }
    m, n := row - 1, col + 1
    for m >= 0 && n < len(board[0]) {
        if board[m][n] == "Q" {
            return false
        }
        m--
        n++
    }
    return true
}
```
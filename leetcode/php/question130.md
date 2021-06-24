```
给你一个 m x n 的矩阵 board ，由若干字符 'X' 和 'O' ，找到所有被 'X' 围绕的区域，并将这些区域里所有的 'O' 用 'X' 填充。
 
示例 1：
输入：board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]
输出：[["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
解释：被围绕的区间不会存在于边界上，换句话说，任何边界上的 'O' 都不会被填充为 'X'。 任何不在边界上，或不与边界上的 'O' 相连的 'O' 最终都会被填充为 'X'。如果两个元素在水平或垂直方向相邻，则称它们是“相连”的。
示例 2：

输入：board = [["X"]]
输出：[["X"]]
 
提示：
m == board.length
n == board[i].length
1 <= m, n <= 200
board[i][j] 为 'X' 或 'O'
```

```
<?php
class Solution {

    /**
     * @param String[][] $board
     * @return NULL
     */
    function solve(&$board) {
        foreach ($board as $key1 => $value1) {
            foreach ($value1 as $key2 => $value2) {
                if (($key1 == 0 || $key2 == 0 || $key1 == count($board) - 1 || $key2 == count($board[0]) - 1) && $value2 == 'O') {
                    self::dfs($board, $key1, $key2);
                }
            }
        }
        foreach ($board as $key3 => $value3) {
            foreach ($value3 as $key4 => $value4) {
                if ($value4 == 'O') {
                    $board[$key3][$key4] = 'X';
                }
                if ($value4 == '#') {
                    $board[$key3][$key4] = 'O';
                }
            }
        }
        
        return $board;
    }

    function dfs(&$board, $m, $n) {
        if ($m < 0 || $n < 0 || $m >= count($board) || $n >= count($board[0]) || $board[$m][$n] == 'X' || $board[$m][$n] == '#') {
            return;
        }
        $board[$m][$n] = '#';
        self::dfs($board, $m + 1, $n, $biao);
        self::dfs($board, $m, $n + 1, $biao);
        self::dfs($board, $m - 1, $n, $biao);
        self::dfs($board, $m, $n - 1, $biao);
    }
}
```
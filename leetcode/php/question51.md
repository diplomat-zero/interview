```
按照国际象棋的规则，皇后可以攻击与之处在同一行或同一列或同一斜线上的棋子。

n 皇后问题 研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。

给你一个整数 n ，返回所有不同的 n 皇后问题 的解决方案。

每一种解法包含一个不同的 n 皇后问题 的棋子放置方案，该方案中 'Q' 和 '.' 分别代表了皇后和空位。

 

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
class Solution {

    /**
     * @param Integer $n
     * @return String[][]
     */
    function solveNQueens($n) {
      for ($i = 0; $i < $n; $i++) {
            for ($j = 0; $j < $n; $j++) {
                $board[$i][$j] = '.';
            }
        }
        $res = [];
        $this->dfs($board, 0, $res);
        $ret = [];
        foreach ($res as $value) {
            $tmp_res = [];
            foreach ($value as $value1) {
                $tmp = implode('', $value1);
                $tmp_res[] = $tmp;
            }
            $ret[] = $tmp_res;
        }
        return $ret;
    }

    function dfs(&$board, $row, &$res) {
        if (count($board) == $row) {
            $res[] = $board;
            return;
        }
        $n = count($board[$row]);
        for ($col = 0; $col < $n; $col++) {
            if ($this->isValid($board, $row, $col)) {
                $board[$row][$col] = 'Q';
                $this->dfs($board, $row + 1,$res);
                $board[$row][$col] = '.';
            }
        }
    }
    
    function isValid($board, $row, $col) {
        $n = count($board);
        for ($i = 0; $i < $n; $i++) {
            if ($board[$row][$i] == 'Q') {
                return false;
            }
            if ($board[$i][$col] == 'Q') {
                return false;
            }
        }
        for ($i = $row - 1, $j = $col + 1; $i >= 0 && $j < $n; $i--,$j++) {
            if ($board[$i][$j] == 'Q') {
                return false;
            }
        }
        for ($i = $row - 1, $j = $col - 1; $i >= 0 && $j >= 0; $i--,$j--) {
            if ($board[$i][$j] == 'Q') {
                return false;
            }
        }
        return true;
    }
}
```
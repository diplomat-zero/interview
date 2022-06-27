```
n 皇后问题 研究的是如何将 n 个皇后放置在 n × n 的棋盘上，并且使皇后彼此之间不能相互攻击。

给你一个整数 n ，返回 n 皇后问题 不同的解决方案的数量。

 

示例 1：


输入：n = 4
输出：2
解释：如上图所示，4 皇后问题存在两个不同的解法。
示例 2：

输入：n = 1
输出：1
 

提示：

1 <= n <= 9
```

```

```

```
class Solution {

    /**
     * @param Integer $n
     * @return Integer
     */
    function totalNQueens($n) {
        for ($i = 0; $i < $n; $i++) {
            for ($j = 0; $j < $n; $j++) {
                $board[$i][$j] = '.';
            }
        }
        $res = [];
        $this->dfs($board, 0, $res);
        return count($res);
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
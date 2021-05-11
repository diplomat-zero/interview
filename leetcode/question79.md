```
给定一个 m x n 二维字符网格 board 和一个字符串单词 word 。如果 word 存在于网格中，返回 true ；否则，返回 false 。
单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

示例 1：
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：true

示例 2：
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
输出：true

示例 3：
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
输出：false
 
提示：
m == board.length
n = board[i].length
1 <= m, n <= 6
1 <= word.length <= 15
board 和 word 仅由大小写英文字母组成
进阶：你可以使用搜索剪枝的技术来优化解决方案，使其在 board 更大的情况下可以更快解决问题？
```

```
<?php
class Solution {

    /**
     * @param String[][] $board
     * @param String $word
     * @return Boolean
     */
    function exist($board, $word) {
        $first = substr($word, 0, 1);
        foreach ($board as $key1 => $value1) {
            foreach ($value1 as $key2 => $value2) {
                if ($value2 == $first) {
                    $find[] = [$key1, $key2];
                }
            }
        }
        
        foreach ($find as $value3) {
            $visited = [];
            $visited[$value3[0]][$value3[1]] = true;
            $find = false;
            self::dfs($board, $value3[0], $value3[1], $word, 1, $visited, $find);
            if ($find) {
                return true;
            }
        }

        return false;
    }

    function dfs($board, $m, $n, $word, $position, &$visited, &$find) {
        if (strlen($word) == $position) {
            $find = true;
        }

        if (isset($board[$m + 1][$n])) {
            if (!$visited[$m + 1][$n]) {
                $tmp1 = $board[$m + 1][$n];
                if ($tmp1 == $word[$position]) {
                    $visited[$m + 1][$n] = true;
                    self::dfs($board, $m + 1, $n, $word, $position + 1, $visited, $find);
                    $visited[$m + 1][$n] = false;
                }
            } 
        }
        if (isset($board[$m][$n + 1])) {
            if (!$visited[$m][$n + 1]) {
                $tmp2 = $board[$m][$n + 1];
                if ($tmp2 == $word[$position]) {
                    $visited[$m][$n + 1] = true;
                    self::dfs($board, $m, $n + 1, $word, $position + 1, $visited, $find);
                    $visited[$m][$n + 1] = false;
                }
            }
        }
        if (isset($board[$m - 1][$n])) {
            if (!$visited[$m - 1][$n]) {
                $tmp3 = $board[$m - 1][$n];
                if ($tmp3 == $word[$position]) {
                    $visited[$m - 1][$n] = true;
                    self::dfs($board, $m - 1, $n, $word, $position + 1, $visited, $find);
                    $visited[$m - 1][$n] = false;
                }
            }
        }
        if (isset($board[$m][$n - 1])) {
            if (!$visited[$m][$n - 1]) {
                $tmp4 = $board[$m][$n - 1];
                if ($tmp4 == $word[$position]) {
                    $visited[$m][$n - 1] = true;
                    self::dfs($board, $m, $n - 1, $word, $position + 1, $visited, $find);
                    $visited[$m][$n - 1] = false;
                }
            } 
        }
    }
}
```
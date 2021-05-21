```
给你一个由 '1'（陆地）和 '0'（水）组成的的二维网格，请你计算网格中岛屿的数量。
岛屿总是被水包围，并且每座岛屿只能由水平方向和/或竖直方向上相邻的陆地连接形成。
此外，你可以假设该网格的四条边均被水包围。

示例 1：
输入：grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
输出：1

示例 2：
输入：grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
输出：3
 
提示：
m == grid.length
n == grid[i].length
1 <= m, n <= 300
grid[i][j] 的值为 '0' 或 '1'
```

```
<?php
class Solution {

    /**
     * @param String[][] $grid
     * @return Integer
     */
    function numIslands($grid) {
        $len1 = count($grid);
        $len2 = count($grid[0]);
        $count = 0;
        foreach ($grid as $key1 => &$value1) {
            foreach ($value1 as $key2 => &$value2) {
                if ($value2 == '1') {
                    self::dfs($grid, $key1, $key2, $len1, $len2);
                    $count++;
                }
            }
        }
        return $count;
    }

    function dfs(&$grid, $m, $n, $len1, $len2) {
        if ($m < 0 || $n < 0 || $m >= $len1 || $n >= $len2 || $grid[$m][$n] == '0' || $grid[$m][$n] == '#') {
            return;
        }
        $grid[$m][$n] = '#';
        self::dfs($grid, $m + 1, $n, $len1, $len2);
        self::dfs($grid, $m - 1, $n, $len1, $len2);
        self::dfs($grid, $m, $n + 1, $len1, $len2);
        self::dfs($grid, $m, $n - 1, $len1, $len2);
    }
}
```
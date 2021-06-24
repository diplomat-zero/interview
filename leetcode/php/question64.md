```
给定一个包含非负整数的 m x n 网格 grid ，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。
说明：每次只能向下或者向右移动一步。

示例 1：
输入：grid = [[1,3,1],[1,5,1],[4,2,1]]
输出：7
解释：因为路径 1→3→1→1→1 的总和最小。

示例 2：
输入：grid = [[1,2,3],[4,5,6]]
输出：12
 
提示：
m == grid.length
n == grid[i].length
1 <= m, n <= 200
0 <= grid[i][j] <= 100
```

```
<?php
class Solution {

    /**
     * @param Integer[][] $grid
     * @return Integer
     */
    function minPathSum($grid) {
        $dp = [];
        $m = count($grid);
        $n = count($grid[0]);
        $dp[0][0] = $grid[0][0];
        for ($i = 1; $i < $n; $i++) {
            $dp[0][$i] = $dp[0][$i - 1] + $grid[0][$i];
        }
        for ($j = 1; $j < $m; $j++) {
            $dp[$j][0] = $dp[$j - 1][0] + $grid[$j][0];
        }
        for ($p = 1; $p < $m; $p++) {
            for ($q = 1; $q < $n; $q++) {
                $dp[$p][$q] = $grid[$p][$q] + min($dp[$p - 1][$q], $dp[$p][$q - 1]);
            }
        }
        
        return $dp[$m - 1][$n - 1];
    }
}
```
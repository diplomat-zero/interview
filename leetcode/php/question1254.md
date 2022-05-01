```
二维矩阵 grid 由 0 （土地）和 1 （水）组成。岛是由最大的4个方向连通的 0 组成的群，封闭岛是一个 完全 由1包围（左、上、右、下）的岛。
请返回 封闭岛屿 的数目。

示例 1：
输入：grid = [[1,1,1,1,1,1,1,0],[1,0,0,0,0,1,1,0],[1,0,1,0,1,1,1,0],[1,0,0,0,0,1,0,1],[1,1,1,1,1,1,1,0]]
输出：2
解释：
灰色区域的岛屿是封闭岛屿，因为这座岛屿完全被水域包围（即被 1 区域包围）。

示例 2：
输入：grid = [[0,0,1,0,0],[0,1,0,1,0],[0,1,1,1,0]]
输出：1

示例 3：
输入：grid = [[1,1,1,1,1,1,1],
             [1,0,0,0,0,0,1],
             [1,0,1,1,1,0,1],
             [1,0,1,0,1,0,1],
             [1,0,1,1,1,0,1],
             [1,0,0,0,0,0,1],
             [1,1,1,1,1,1,1]]
输出：2
 
提示：
1 <= grid.length, grid[0].length <= 100
0 <= grid[i][j] <=1
```

```
class Solution {

    /**
     * @param Integer[][] $grid
     * @return Integer
     */
    function closedIsland($grid) {
        for ($m = 0; $m < count($grid); $m++) {
            if ($grid[$m][0] == 0) {
                $this->dfs($grid, $m, 0);
            }
            if ($grid[$m][count($grid[0]) - 1] == 0) {
                $this->dfs($grid, $m, count($grid[0]) - 1);
            }
        }
        for ($n = 0; $n < count($grid[0]); $n++) {
            if ($grid[0][$n] == 0) {
                $this->dfs($grid, 0, $n);
            }
            if ($grid[count($grid) - 1][$n] == 0) {
                $this->dfs($grid, count($grid) - 1, $n);
            }
        }

        $count = 0;
        for ($p = 0; $p < count($grid); $p++) {
            for ($q = 0; $q < count($grid[0]); $q++) {
                if ($grid[$p][$q] == 0) {
                    $count++;
                    $this->dfs($grid, $p, $q);
                }
            }
        }
        return $count;
    }

    function dfs(&$grid, $i, $j) {
        if ($i < 0 || $j < 0 || $i >= count($grid) || $j >= count($grid[0]) || $grid[$i][$j] == 1) {
            return;
        }

        $grid[$i][$j] = 1;
        $this->dfs($grid, $i + 1, $j);
        $this->dfs($grid, $i - 1, $j);
        $this->dfs($grid, $i, $j + 1);
        $this->dfs($grid, $i, $j - 1);
    }
}
```
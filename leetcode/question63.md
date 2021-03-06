```
一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

网格中的障碍物和空位置分别用 1 和 0 来表示。

示例 1：
输入：obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]
输出：2
解释：
3x3 网格的正中间有一个障碍物。
从左上角到右下角一共有 2 条不同的路径：
1. 向右 -> 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右 -> 向右


输入：obstacleGrid = [[0,1],[0,0]]
输出：1

提示：
m == obstacleGrid.length
n == obstacleGrid[i].length
1 <= m, n <= 100
obstacleGrid[i][j] 为 0 或 1
```

```
class Solution {

    /**
     * @param Integer[][] $obstacleGrid
     * @return Integer
     */
    function uniquePathsWithObstacles($obstacleGrid) {
        $m = count($obstacleGrid, 0);
        $n = count($obstacleGrid[0]);
        $a = [];

        $x_true = false;
        for ($i = 0; $i < $m; $i++) {
            if ($x_true) {
                $a[$i][0] = 0;
                continue;
            }
            if ($obstacleGrid[$i][0] == 1) {
                $a[$i][0] = 0;
                $x_true = true;
            } else {
                $a[$i][0] = 1;
            }
        }

        $y_true = false;
        for ($j = 0; $j < $n; $j++) {
            if ($y_true) {
                $a[0][$j] = 0;
                continue;
            }
            if ($obstacleGrid[0][$j] == 1) {
                $a[0][$j] = 0;
                $y_true = true;
            } else {
                $a[0][$j] = 1;
            }
        }

        for ($i = 1; $i < $m; $i++) {
            for ($j = 1; $j < $n; $j++) {
                if ($obstacleGrid[$i][$j] == 1) {
                    $a[$i][$j] = 0;
                    continue;
                }
                $a[$i][$j] = $a[$i - 1][$j] + $a[$i][$j - 1];
            }
        }

        return $a[$m - 1][$n - 1];
    }
}
```
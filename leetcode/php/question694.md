```
给定一个非空 01 二维数组表示的网格，一个岛屿由四连通（上、下、左、右四个方向）的 1 组成，你可以认为网格的四周被海水包围。
请你计算这个网格中共有多少个形状不同的岛屿。两个岛屿被认为是相同的，当且仅当一个岛屿可以通过平移变换（不可以旋转、翻转）和另一个岛屿重合。

示例 1：
11000
11000
00011
00011
给定上图，返回结果 1 。

示例 2：
11011
10000
00001
11011
给定上图，返回结果 3 。

注意：
11
1
和
 1
11
是不同的岛屿，因为我们不考虑旋转、翻转操作。

提示：二维数组每维的大小都不会超过 50 。
```

```
思路
DFS
```

```
class Solution {

    /**
     * @param Integer[][] $grid
     * @return Integer
     */
    function numDistinctIslands($grid) {
        $map = [];
        for ($i = 0; $i < count($grid); $i++) {
            for ($j = 0; $j < count($grid[0]); $j++) {
                if ($grid[$i][$j] == 1) {
                    $res = '';
                    $this->dfs($grid, $i, $j, $res, 100);
                    if (!in_array($res, $map)) {
                        $map[] = $res;
                   }
                }
            }
        }
        return count($map);
    }

    function dfs(&$grid, $i, $j, &$res, $dir) {
        if ($i < 0 || $j < 0 || $i >= count($grid) || $j >= count($grid[0]) || $grid[$i][$j] == 0) {
            return;
        }

        $grid[$i][$j] = 0;
        $res .= $dir . ',';
        $this->dfs($grid, $i + 1, $j, $res, 1);
        $this->dfs($grid, $i - 1, $j, $res, 2);
        $this->dfs($grid, $i, $j + 1, $res, 3);
        $this->dfs($grid, $i, $j - 1, $res, 4);
        $res .= -$dir . ',';
    }
}
```
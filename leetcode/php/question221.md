```
在一个由 '0' 和 '1' 组成的二维矩阵内，找到只包含 '1' 的最大正方形，并返回其面积。

示例 1：
输入：matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
输出：4

示例 2：
输入：matrix = [["0","1"],["1","0"]]
输出：1

示例 3：
输入：matrix = [["0"]]
输出：0
 

提示：
m == matrix.length
n == matrix[i].length
1 <= m, n <= 300
matrix[i][j] 为 '0' 或 '1'
```

```
class Solution {

    /**
     * @param String[][] $matrix
     * @return Integer
     */
    function maximalSquare($matrix) {
        if (empty($matrix)) {
            return 0;
        }
        $dp = [];
        for ($i = 0; $i < count($matrix); $i++) {
            $dp[$i][0] = $matrix[$i][0];
        }

        for ($j = 0; $j < count($matrix[0]); $j++) {
            $dp[0][$j] = $matrix[0][$j];
        }

        $max = PHP_INT_MIN;
        for ($m = 0; $m < count($matrix); $m++) {
            for ($n = 0; $n < count($matrix[0]); $n++) {
                if ($matrix[$m][$n] == 0) {
                    $dp[$m][$n] = 0;
                } else {
                    $dp[$m][$n] = min($dp[$m - 1][$n], $dp[$m][$n - 1], $dp[$m - 1][$n - 1]) + 1;
                    $max = max($max, $dp[$m][$n]);
                }
            }
        }
        return $max == PHP_INT_MIN ? 0 : $max * $max;
    }
}
```
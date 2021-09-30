```
给你一个 m 行 n 列的矩阵 matrix ，请按照 顺时针螺旋顺序 ，返回矩阵中的所有元素。

示例 1：
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]

示例 2：
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
 
提示：
m == matrix.length
n == matrix[i].length
1 <= m, n <= 10
-100 <= matrix[i][j] <= 100
```

```
class Solution {

    /**
     * @param Integer[][] $matrix
     * @return Integer[]
     */
    function spiralOrder($matrix) {
        $left = 0;
        $right = count($matrix[0]) - 1;
        $top = 0;
        $bottom = count($matrix) - 1;
        $total = count($matrix) * count($matrix[0]);
        $ret = [];

        while ($total >= 1) {
            for ($i = $left; $i <= $right && $total >= 1; $i++) {
                $ret[] = $matrix[$top][$i];
                $total--;
            }
            $top++;
            for ($i = $top; $i <= $bottom && $total >= 1; $i++) {
                $ret[] = $matrix[$i][$right];
                $total--;
            }
            $right--;
            for ($i = $right; $i >= $left && $total >= 1; $i--) {
                $ret[] = $matrix[$bottom][$i];
                $total--;
            }
            $bottom--;
            for ($i = $bottom; $i >= $top && $total >= 1; $i--) {
                $ret[] = $matrix[$i][$left];
                $total--;
            }
            $left++;
        }
        
        return $ret;
    }
}
```
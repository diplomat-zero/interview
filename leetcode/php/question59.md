```
给你一个正整数 n ，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的 n x n 正方形矩阵 matrix 。

示例 1：
输入：n = 3
输出：[[1,2,3],[8,9,4],[7,6,5]]

示例 2：
输入：n = 1
输出：[[1]]
 
提示：
1 <= n <= 20
```

```

```

```
class Solution {

    /**
     * @param Integer $n
     * @return Integer[][]
     */
    function generateMatrix($n) {
        $left = 0;
        $right = $n - 1;
        $top = 0;
        $bottom = $n - 1;
        $total = $n * $n;
        $result = array_fill(0, $n, array_fill(0, $n, 0));
        $cur = 1;
        while ($cur <= $total) {
            for ($i = $left; $i <= $right && $cur <= $total; $i++) {
                $result[$top][$i] = $cur;
                $cur++;
            }
            $top++;

            for ($i = $top; $i <= $bottom && $cur <= $total; $i++) {
                $result[$i][$right] = $cur;
                $cur++;
            }
            $right--;

            for ($i = $right; $i >= $left && $cur <= $total; $i--) {
                $result[$bottom][$i] = $cur;
                $cur++;
            }
            $bottom--;

            for ($i = $bottom; $i >= $top && $cur <= $total; $i--) {
                $result[$i][$left] = $cur;
                $cur++;
            }
            $left++;
        }
        return $result;
    }
}
```
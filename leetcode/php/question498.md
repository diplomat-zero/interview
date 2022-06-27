```
给你一个大小为 m x n 的矩阵 mat ，请以对角线遍历的顺序，用一个数组返回这个矩阵中的所有元素。

 

示例 1：


输入：mat = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,4,7,5,3,6,8,9]
示例 2：

输入：mat = [[1,2],[3,4]]
输出：[1,2,3,4]
 

提示：

m == mat.length
n == mat[i].length
1 <= m, n <= 104
1 <= m * n <= 104
-105 <= mat[i][j] <= 105
```

```

```

```
class Solution {

    /**
     * @param Integer[][] $mat
     * @return Integer[]
     */
    function findDiagonalOrder($mat) {
        $res = [];
        for ($i = 0; $i < count($mat); $i++) {
            for ($j = 0; $j < count($mat[0]); $j++) {
                $res[$i + $j][] = $mat[$i][$j];
            }
        }
        $ret = [];
        for ($m = 0; $m < count($res); $m++) {
            if ($m % 2 == 0) {
                for ($n = count($res[$m]) - 1; $n >= 0; $n--) {
                    $ret[] = $res[$m][$n];
                }
            } else {
                for ($n = 0; $n < count($res[$m]); $n++) {
                    $ret[] = $res[$m][$n];
                }
            }
        }
        return $ret;
    }
}
```
```
给定一个 n × n 的二维矩阵表示一个图像。将图像顺时针旋转 90 度。
说明：
你必须在原地旋转图像，这意味着你需要直接修改输入的二维矩阵。请不要使用另一个矩阵来旋转图像。

示例 1:
给定 matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],
原地旋转输入矩阵，使其变为:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]

示例 2:
给定 matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

原地旋转输入矩阵，使其变为:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```

```
class Solution {

    /**
     * @param Integer[][] $matrix
     * @return NULL
     */
    function rotate(&$matrix) {
        for ($i = 0; $i < count($matrix); $i++) {
            for ($j = $i + 1; $j < count($matrix); $j++) {
                $tmp = $matrix[$i][$j];
                $matrix[$i][$j] = $matrix[$j][$i];
                $matrix[$j][$i] = $tmp;
            }
        }
        foreach ($matrix as &$value) {
            $start = 0;
            $end = count($value) - 1;
            while ($start < $end) {
                $tmp1 = $value[$start];
                $value[$start] = $value[$end];
                $value[$end] = $tmp1;
                $start++;
                $end--;
            }
        }
    }
}
```

```
class Solution {
    /**
     * @param Integer[][] $matrix
     *
     * @return NULL
     */
    function rotate(&$matrix) {
        $count_matrix = count($matrix);
        for ($i = 0; $i < $count_matrix / 2; $i++) {
            $rotate_count = $count_matrix - $i - 1;
            for ($j = $i; $j < $rotate_count; $j++) {
                $temp = $matrix[$i][$j];
                $matrix[$i][$j] = $matrix[$count_matrix - 1 - $j][$i];
                $matrix[$count_matrix - 1 - $j][$i] = $matrix[$count_matrix - 1 - $i][$count_matrix - 1 - $j];
                $matrix[$count_matrix - 1 - $i][$count_matrix - 1 - $j] = $matrix[$j][$count_matrix - 1 - $i];
                $matrix[$j][$count_matrix - 1 - $i] = $temp;
            }
        }

        return $matrix;
    }
}
```
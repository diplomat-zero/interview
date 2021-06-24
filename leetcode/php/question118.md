```
给定一个非负整数 numRows，生成杨辉三角的前 numRows 行。

在杨辉三角中，每个数是它左上方和右上方的数的和。

示例:

输入: 5
输出:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1],
[1,5,10,10,5,1]
]
```

```
class Solution {

    /**
     * @param Integer $numRows
     * @return Integer[][]
     */
    function generate($numRows) {
        $nums = [];

        for ($i = 0; $i < $numRows; $i++) {
            for ($j = 0; $j <= $i; $j++) {
                if ($j == 0 || $j == $i) {
                    $nums[$i][$j] = 1;
                } else {
                    $a = isset($nums[$i - 1][$j - 1]) ? $nums[$i - 1][$j - 1] : 0;
                    $b = isset($nums[$i - 1][$j]) ? $nums[$i - 1][$j] : 0;
                    $nums[$i][$j] = $a + $b;
                }
            }
        }

        return $nums;
    }
}
```
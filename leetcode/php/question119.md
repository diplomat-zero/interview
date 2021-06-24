```
给定一个非负索引 k，其中 k ≤ 33，返回杨辉三角的第 k 行。

在杨辉三角中，每个数是它左上方和右上方的数的和。

示例:

输入: 3
输出: [1,3,3,1]
进阶：

你可以优化你的算法到 O(k) 空间复杂度吗？
```

```
class Solution {

    /**
     * @param Integer $rowIndex
     * @return Integer[]
     */
    function getRow($rowIndex) {
        $nums = [];

        for ($i = 0; $i <= $rowIndex; $i++) {
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

        return $nums[$rowIndex];
    }
}
```
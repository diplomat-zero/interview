```
出一个区间的集合，请合并所有重叠的区间。

示例 1:
输入: intervals = [[1,3],[2,6],[8,10],[15,18]]
输出: [[1,6],[8,10],[15,18]]
解释: 区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].

示例 2:
输入: intervals = [[1,4],[4,5]]
输出: [[1,5]]
解释: 区间 [1,4] 和 [4,5] 可被视为重叠区间。
```

```
class Solution {

    /**
     * @param Integer[][] $intervals
     * @return Integer[][]
     */
    function merge($intervals) {
        $len = count($intervals);
        for ($i = 0; $i < $len; $i++) {
            for ($j = $i + 1; $j < $len; $j++) {
                if (isset($intervals[$j]) && ($intervals[$i][1] >= $intervals[$j][0]) && ($intervals[$i][0] <= $intervals[$j][1])) {
                    $x = $intervals[$i][0] > $intervals[$j][0] ? $intervals[$j][0] : $intervals[$i][0];
                    $y = $intervals[$i][1] > $intervals[$j][1] ? $intervals[$i][1] : $intervals[$j][1];
                    $intervals[$j] = [$x, $y];
                    unset($intervals[$i]);
                    break;
                } else {
                    $intervals[$j] = [$intervals[$j][0], $intervals[$j][1]];
                }
            }
        }

        return array_values($intervals);
    }
}
```
```
给出一个无重叠的 ，按照区间起始端点排序的区间列表。

在列表中插入一个新的区间，你需要确保列表中的区间仍然有序且不重叠（如果有必要的话，可以合并区间）。

 

示例 1：
输入：intervals = [[1,3],[6,9]], newInterval = [2,5]
输出：[[1,5],[6,9]]

示例 2：
输入：intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
输出：[[1,2],[3,10],[12,16]]
解释：这是因为新的区间 [4,8] 与 [3,5],[6,7],[8,10] 重叠。
```

```
class Solution {

    /**
     * @param Integer[][] $intervals
     * @param Integer[] $newInterval
     * @return Integer[][]
     */
    function insert($intervals, $newInterval) {
        if (empty($intervals)) {
            return [$newInterval];
        }

        $insert = true;
        $len = count($intervals);
        for ($i = 0; $i < $len; $i++) {
            if ($intervals[$i][1] >= $newInterval[0]) {
                array_splice($intervals, $i, 0, [$newInterval]);
                $insert = false;
                break;
            }
        }

        if ($insert) {
            array_push( $intervals, $newInterval);
            return $intervals;
        }

        $new_len = count($intervals);
        for ($i = 0; $i < $new_len; $i++) {
            for ($j = $i + 1; $j < $new_len; $j++) {
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
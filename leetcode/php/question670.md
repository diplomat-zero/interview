```
给定一个非负整数，你至多可以交换一次数字中的任意两位。返回你能得到的最大值。

示例 1 :
输入: 2736
输出: 7236
解释: 交换数字2和数字7。

示例 2 :
输入: 9973
输出: 9973
解释: 不需要交换。

注意:
给定数字的范围是 [0, 108]
```

```

```

```
class Solution {

    /**
     * @param Integer $num
     * @return Integer
     */
    function maximumSwap($num) {
        $num = (string)$num;
        for ($i = 0; $i < strlen($num); $i++) {
            $list[] = $num[$i];
        }
        rsort($list);
        for ($j = 0; $j < count($list); $j++) {
            if ($num[$j] != $list[$j]) {
                $swap_a = $j;
                $start = count($list) - 1;
                while ($num[$start] != $list[$j]) {
                    $start--;
                }
                $swap_b = $start;
                break;
            }
        }
        $tmp = $num[$swap_a];
        $num[$swap_a] = $num[$swap_b];
        $num[$swap_b] = $tmp;
        return $num;
    }
}
```
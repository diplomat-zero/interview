```
给你两个二进制字符串，返回它们的和（用二进制表示）。

输入为 非空 字符串且只包含数字 1 和 0。

 

示例 1:
输入: a = "11", b = "1"
输出: "100"

示例 2:
输入: a = "1010", b = "1011"
输出: "10101"
 

提示：
每个字符串仅由字符 '0' 或 '1' 组成。
1 <= a.length, b.length <= 10^4
字符串如果不是 "0" ，就都不含前导零。
```

```
class Solution {

    /**
     * @param String $a
     * @param String $b
     * @return String
     */
    function addBinary($a, $b) {
        $c = '';
        $len_a = strlen($a);
        $len_b = strlen($b);

        $i = $len_a - 1;
        $j = $len_b - 1;
        $bit = 0;
        while ($i >= 0 || $j >= 0) {
            $i < 0 && $a[$i] = 0;
            $j < 0 && $b[$j] = 0;
            $tmp = $a[$i] + $b[$j] + $bit;
            if ($tmp == 3) {
                $bit = 1;
                $tmp = 1;
            } elseif ($tmp == 2) {
                $bit = 1;
                $tmp = 0;
            } else {
                $bit = 0;
            }
            $c = $tmp . $c;
            $i--;
            $j--;
        }

        if ($bit == 1) {
            $c = $bit . $c;
        }
        return $c;
    }
}
```
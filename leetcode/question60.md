```
给出集合 [1,2,3,...,n]，其所有元素共有 n! 种排列。
按大小顺序列出所有排列情况，并一一标记，当 n = 3 时, 所有排列如下：
"123"
"132"
"213"
"231"
"312"
"321"
给定 n 和 k，返回第 k 个排列。

示例 1：
输入：n = 3, k = 3
输出："213"

示例 2：
输入：n = 4, k = 9
输出："2314"

示例 3：
输入：n = 3, k = 1
输出："123"
 
提示：
1 <= n <= 9
1 <= k <= n!
```
```
<?php
class Solution {

    /**
     * @param Integer $n
     * @param Integer $k
     * @return String
     */
    function getPermutation($n, $k) {
        for ($i = 1; $i <= $n; $i++) {
            $num[$i] = $i;
        }
        $result = '';
        self::digui($num, $k, $result);
        return $result;
    }

    function digui($num, $k, &$result) {
        $num = array_values($num);
        $len = count($num);
        if ($len == 1) {
            $key = array_pop($num);
            $result = $result . $key;
            return $result;
        }
        $count = self::jie($len - 1);
        for ($i = 0; $i < $len; $i++) {
            $tmp_count_left = $count * $i;
            $tmp_count_right = $count * ($i + 1);
            if ($tmp_count_left < $k && $k <= $tmp_count_right) {
                $find = $i;
                $left_k = $k - $tmp_count_left;
            }
        }
        $result .= $num[$find];
        unset($num[$find]);
        self::digui($num, $left_k, $result);
    }

    function jie($n) {
        $dp[0] = 1;
        $dp[1] = 1;
        $dp[2] = 2;
        for ($i = 3; $i <= $n; $i++) {
            $dp[$i] = $i * $dp[$i - 1];
        }
        return $dp[$n];
    }
}
```

```
<?php
class Solution {

    /**
     * @param Integer $n
     * @param Integer $k
     * @return String
     */
    function getPermutation($n, $k) {
        $count = self::jie($n - 1);
        for ($i = 1; $i <= $n; $i++) {
            $num[$i] = $i;
            $tmp_count_left = $count * ($i - 1);
            $tmp_count_right = $count * $i;
            if ($tmp_count_left < $k && $k <= $tmp_count_right) {
                $find = $i;
                $left_k = $k - $tmp_count_left;
            }
        }
        $result = '';
        unset($num[$find]);
        $j = 0;
        self::dfs(array_values($num), '', $j, $left_k, $result);
        return $find.$result;
    }

    function dfs($num, $trace, &$j, $k, &$result) {
        if (strlen($trace) == count($num)) {
            $j++;
            if ($j == $k) {
                $result = $trace;
            }
        }

        for ($i = 0; $i < count($num); $i++) {
            if (strlen($trace) <= count($num)) {
                $find = (string)$num[$i];
                if (strpos($trace, $find) === false) {
                    $trace .= $num[$i];
                    self::dfs($num, $trace, $j, $k, $result);
                    $trace = substr($trace, 0, strlen($trace) - 1);
                }
            } 
        }
    }

    function jie($n) {
        $dp[0] = 1;
        $dp[1] = 1;
        $dp[2] = 2;
        for ($i = 3; $i <= $n; $i++) {
            $dp[$i] = $i * $dp[$i - 1];
        }
        return $dp[$n];
    }
}
```
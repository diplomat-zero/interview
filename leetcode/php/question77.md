```
给定两个整数 n 和 k，返回 1 ... n 中所有可能的 k 个数的组合。

示例:
输入: n = 4, k = 2
输出:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

```
<?php
class Solution {

    /**
     * @param Integer $n
     * @param Integer $k
     * @return Integer[][]
     */
    function combine($n, $k) {
        $result = [];
        self::dfs($n, [], $k, $result, 1);
        return $result;
    }

    function dfs($n, $trace, $k, &$result, $start) {
        if (count($trace) == $k) {
            $result[] = $trace;
        }

        for ($i = $start; $i <= ($n - ($k - count($trace)) + 1); $i++) {
            if (!in_array($i, $trace) && count($trace) <= $k) {
                $trace[] = $i;
                self::dfs($n, $trace, $k, $result, $i + 1);
                array_pop($trace);
            }  
        }
    }
}
```
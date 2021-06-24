```
数字 n 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 有效的 括号组合。

示例 1：
输入：n = 3
输出：["((()))","(()())","(())()","()(())","()()()"]

示例 2：
输入：n = 1
输出：["()"]
 
提示：
1 <= n <= 8
```

```
超时 待优化
<?php
class Solution {

    /**
     * @param Integer $n
     * @return String[]
     */
    function generateParenthesis($n) {
        $i = 0;
        while ($i < $n) {
            $num .= '()';
            $i++;
        }
        $result = [];
        self::dfs($num , '',$result, $n);
        return $result;
    }

    function dfs($num, $trace, &$result, $n) {
        if (strlen($num) == strlen($trace)) {
            if (!in_array($trace, $result)) {
                $result[] = $trace;
            }
            return;
        }
        for ($i = 0; $i < strlen($num); $i++) {
            if (substr_count($trace, $num[$i]) == $n || substr_count($trace, ')') > substr_count($trace, '(')) {
                continue;
            }
            $trace .= $num[$i];
            self::dfs($num, $trace, $result, $n);
            $trace = substr($trace, 0, strlen($trace) - 1);
        }
    }
}
```
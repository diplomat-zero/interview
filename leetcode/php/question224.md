```
给你一个字符串表达式 s ，请你实现一个基本计算器来计算并返回它的值。
注意:不允许使用任何将字符串作为数学表达式计算的内置函数，比如 eval() 。

示例 1：
输入：s = "1 + 1"
输出：2

示例 2：
输入：s = " 2-1 + 2 "
输出：3

示例 3：
输入：s = "(1+(4+5+2)-3)+(6+8)"
输出：23
 
提示：
1 <= s.length <= 3 * 105
s 由数字、'+'、'-'、'('、')'、和 ' ' 组成
s 表示一个有效的表达式
'+' 不能用作一元运算(例如， "+1" 和 "+(2 + 3)" 无效)
'-' 可以用作一元运算(即 "-1" 和 "-(2 + 3)" 是有效的)
输入中不存在两个连续的操作符
每个数字和运行的计算将适合于一个有符号的 32位 整数
```

```

```

```
class Solution {

    /**
     * @param String $s
     * @return Integer
     */

    function calculate($s) {    
        $i = 0;    
        return $this->compute($s,$i);
    }
    function compute($s, &$index) {
        $sign = '+';
        $stack = [];
        $num = 0;
        for (; $index < strlen($s); $index++) {
            $char = $s[$index];
            if (is_numeric($char)) {
                $num = $num * 10 + intval($char);
            } else if ($char == '(') {
                $new_index = $index + 1;
                $num = $this->compute($s, $new_index);
                $index = $new_index;
            }
            if ((!is_numeric($char) && $char != ' ') || $index == (strlen($s) - 1)) {
                if ($sign == '+') {
                    $stack[] = $num;
                } elseif ($sign == '-') {
                    $stack[] = -$num;
                } elseif ($sign == '*') {
                    $end = end($stack);
                    array_pop($stack);
                    $stack[] = $end * $num;
                } elseif ($sign == '/') {
                    $end = end($stack);
                    array_pop($stack);
                    $stack[] = $end / $num;
                }
                $num = 0;
                $sign = $char;
            }
            if ($char == ')') {
                break;
            }
        }
        return array_sum($stack);
    }
}
```
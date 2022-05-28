```
给你一个字符串表达式 s ，请你实现一个基本计算器来计算并返回它的值。

整数除法仅保留整数部分。

你可以假设给定的表达式总是有效的。所有中间结果将在 [-231, 231 - 1] 的范围内。

注意：不允许使用任何将字符串作为数学表达式计算的内置函数，比如 eval() 。

示例 1：
输入：s = "3+2*2"
输出：7

示例 2：
输入：s = " 3/2 "
输出：1

示例 3：
输入：s = " 3+5 / 2 "
输出：5
 
提示：
1 <= s.length <= 3 * 105
s 由整数和算符 ('+', '-', '*', '/') 组成，中间由一些空格隔开
s 表示一个 有效表达式
表达式中的所有整数都是非负整数，且在范围 [0, 231 - 1] 内
题目数据保证答案是一个 32-bit 整数
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
        return $this->compute($s, $i);
    }

    function compute($s, &$index) {
        $stack = [];
        $num = 0;
        $sign = '+';
        for (; $index < strlen($s); $index++) {
            $char = $s[$index];
            if (is_numeric($char)) {
                $num = $num * 10 + intval($char);
            }
            if ($char == '(') {
                $new_index = $index + 1;
                $num = $this->compute($s, $new_index);
                $index = $new_index;
            }
            if ((!is_numeric($char) && $char != ' ') || $index == strlen($s) - 1) {
                if ($sign == '+') {
                    $stack[] = $num;
                } else if ($sign == '-') {
                    $stack[] = -$num;
                } else if ($sign == '*') {
                    $end = end($stack);
                    array_pop($stack);
                    $stack[] = $end * $num;
                } else if ($sign == '/') {
                    $end = end($stack);
                    array_pop($stack);
                    $stack[] = intval($end / $num);
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
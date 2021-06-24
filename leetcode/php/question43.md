```
给定两个以字符串形式表示的非负整数 num1 和 num2，返回 num1 和 num2 的乘积，它们的乘积也表示为字符串形式。

示例 1:
输入: num1 = "2", num2 = "3"
输出: "6"

示例 2:
输入: num1 = "123", num2 = "456"
输出: "56088"

说明：
num1 和 num2 的长度小于110。
num1 和 num2 只包含数字 0-9。
num1 和 num2 均不以零开头，除非是数字 0 本身。
不能使用任何标准库的大数类型（比如 BigInteger）或直接将输入转换为整数来处理。
```

```
<?php
class Solution {

    /**
     * @param String $num1
     * @param String $num2
     * @return String
     */
    function multiply($num1, $num2) {
        if ($num1 == 0 || $num2 == 0) {
            return '0';
        }

        $ret = 0;
        for ($i = strlen($num2) - 1; $i >= 0; $i--) {
            $res = '';
            for ($j = strlen($num1) - 1; $j >= 0; $j--) {
                $tmp = $num1[$j] * $num2[$i] + $jin;
                if ($tmp >= 10) {
                    $jin = floor($tmp / 10);
                } else {
                    $jin = 0;
                }
                $res = substr_replace($res, $tmp % 10, 0, 0); 
            }
            if ($jin != 0) {
                $res = substr_replace($res, $jin, 0, 0); 
                $jin = 0;
            }
            for ($m = 0; $m < strlen($num2) - $i - 1; $m++) {
                $res .= '0';
            }
            $ret = self::sum($ret, $res);
        }

        if ($jin != 0) {
            $ret = substr_replace($ret, $jin, 0, 0);
        }
        return (string)$ret;
    }

    function sum($num1, $num2) {
        $num1 = (string)$num1;
        $num2 = (string)$num2;
        $len_a = strlen($num1) - 1;
        $len_b = strlen($num2) - 1;
        $jin = 0;
        $res = '';
        while ($len_a >= 0 || $len_b >= 0) {
            $tmp_a = $len_a >= 0 ? $num1[$len_a] : 0;
            $tmp_b = $len_b >= 0 ? $num2[$len_b] : 0;
            $tmp = intval($tmp_a) + intval($tmp_b) + intval($jin);
            $num = $tmp % 10;
            if ($tmp >= 10) {
                $jin = 1;
            } else {
                $jin = 0;
            }
            $res = substr_replace($res, $num, 0, 0);
            $len_a--;
            $len_b--;
        }

        if ($jin != 0) {
            $res = substr_replace($res, 1, 0, 0);
        }

        return $res;
    }
}
```
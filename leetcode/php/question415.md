```
给定两个字符串形式的非负整数 num1 和num2 ，计算它们的和。

提示：
num1 和num2 的长度都小于 5100
num1 和num2 都只包含数字 0-9
num1 和num2 都不包含任何前导零
你不能使用任何內建 BigInteger 库， 也不能直接将输入的字符串转换为整数形式。
```

```
class Solution {

    /**
     * @param String $num1
     * @param String $num2
     * @return String
     */
    function addStrings($num1, $num2) {
        $len_a = strlen($num1) - 1;
        $len_b = strlen($num2) - 1;
        $jin = 0;
        $res = '';
        while ($len_a >= 0 || $len_b >= 0) {
            $tmp_a = $len_a >= 0 ? $num1[$len_a] : 0;
            $tmp_b = $len_b >= 0 ? $num2[$len_b] : 0;
            $tmp = $tmp_a + $tmp_b + $jin;
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
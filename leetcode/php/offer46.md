```
给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

示例 1:
输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
 
提示：
0 <= num < 231
```

```
class Solution {

    /**
     * @param Integer $num
     * @return Integer
     */
    function translateNum($num) {
        $len = strlen($num);
        $dp = array_fill(0, $len + 1, 1);
        for ($i = 2; $i <= $len; $i++) {
            $str = substr($num, $i - 2, 2);
            if ($str >= 10 && $str <= 25) {
                $dp[$i] = $dp[$i - 1] + $dp[$i - 2];
            } else {
                $dp[$i] = $dp[$i - 1];
            }
        }

        return $dp[$len];
    }
}
```
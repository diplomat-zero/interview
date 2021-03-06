```
实现 pow(x, n) ，即计算 x 的 n 次幂函数。

示例 1:
输入: 2.00000, 10
输出: 1024.00000

示例 2:
输入: 2.10000, 3
输出: 9.26100

示例 3:
输入: 2.00000, -2
输出: 0.25000
解释: 2-2 = 1/22 = 1/4 = 0.25

说明:
-100.0 < x < 100.0
n 是 32 位有符号整数，其数值范围是 [−231, 231 − 1] 。
```

```
class Solution {

    /**
     * @param Float $x
     * @param Integer $n
     * @return Float
     */
    function myPow($x, $n) {
        $tmp_n = abs($n);
        $ret = 1;
        for ($i = 0; $i < $tmp_n; $i++) {
            $ret = $ret * $x;
        }

        $result = $n > 0 ? $ret : 1 / $ret;
        return $result;
    }
}
```

```
class Solution {

    /**
     * @param Float $x
     * @param Integer $n
     * @return Float
     */
    function myPow($x, $n) {
        if ($n == 0) {
            return 1;
        }
        if ($n == 1) {
            return $x;
        }
        if ($n < 0) {
            $n = -$n;
            $x = 1 / $x;
        }
        if ($n % 2 == 0) {
            $temp = $this->myPow($x, $n / 2);
            return $temp * $temp;
        } else {
            $temp = $this->myPow($x, $n / 2);
            return $temp * $temp * $x;
        }
    }
}
```
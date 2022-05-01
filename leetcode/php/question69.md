```
实现 int sqrt(int x) 函数。

计算并返回 x 的平方根，其中 x 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

示例 1:

输入: 4
输出: 2
示例 2:

输入: 8
输出: 2
说明: 8 的平方根是 2.82842..., 
     由于返回类型是整数，小数部分将被舍去。
```

```
class Solution {

    /**
     * @param Integer $x
     * @return Integer
     */
    function mySqrt($x) {
        if ($x == 1 || $x == 2) {
            return 1;
        }
        $ret = 0;
        for ($i = 1; $i < $x / 2; $i++) {
            if ($i * $i <= $x && $x <= ($i + 1) * ($i + 1)) {
                if ($x == ($i + 1) * ($i + 1)) {
                    return $i + 1;
                }
                $ret = $i;
                break;
            }
        }

        return intval($ret);
    }
}
```

```
class Solution {

    /**
     * @param Integer $x
     * @return Integer
     */
    function mySqrt($x) {
        if ($x <= 1) {
            return $x;
        }
        $left = 1;
        $right = floor($x / 2) + 1;

        while ($left < $right) {
            $mid = floor(($right - $left + 1) / 2 + $left);
            if ($mid > $x / $mid) {
                $right = $mid - 1;
            } else {
                $left = $mid;
            }
        }

        return $left;
    }
}
```
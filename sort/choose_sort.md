```
public static function choose($arr) {
        $length = count($arr);
        if ($length == 0) {
            return $arr;
        }

        for ($i = 0; $i < $length - 1; $i++) {
            $min = $i;
            for ($j = $i + 1; $j < $length; $j++) {
                if ($arr[$j] < $arr[$min]) {
                    $min = $j;
                }
            }
            if ($min != $i) {
                $tmp = $arr[$min];
                $arr[$min] = $arr[$i];
                $arr[$i] = $tmp;
            }
        }

        return $arr;
    }
```
最差时间复杂度-----------O(n^2)

最优时间复杂度-----------O(n^2)

平均时间复杂度-----------O(n^2)

空间复杂度--------------O(1)
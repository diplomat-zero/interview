```
输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。

示例 1:
输入: [10,2]
输出: "102"

示例 2:
输入: [3,30,34,5,9]
输出: "3033459"
 
提示:
0 < nums.length <= 100
说明:

输出结果可能非常大，所以你需要返回一个字符串而不是整数
拼接起来的数字可能会有前导 0，最后结果不需要去掉前导 0
```

```

```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return String
     */
    function minNumber($nums) {
        for ($i = 0; $i < count($nums); $i++) {
            for ($j = $i + 1; $j < count($nums); $j++) {
                $str1 = $nums[$i].$nums[$j];
                $str2 = $nums[$j].$nums[$i];
                if (intval($str1) > intval($str2)) {
                    $tmp = $nums[$i];
                    $nums[$i] = $nums[$j];
                    $nums[$j] = $tmp;
                }
            }
        }
        $res = '';
        foreach ($nums as $num) {
            $res .= $num;
        }
        return $res;
    }
}
```
```
给定一组非负整数 nums，重新排列每个数的顺序（每个数不可拆分）使之组成一个最大的整数。
注意：输出结果可能非常大，所以你需要返回一个字符串而不是整数。

示例 1：
输入：nums = [10,2]
输出："210"

示例 2：
输入：nums = [3,30,34,5,9]
输出："9534330"
 
提示：
1 <= nums.length <= 100
0 <= nums[i] <= 109
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return String
     */
    function largestNumber($nums) {
        $len = count($nums);
        for ($i = 0; $i < $len; $i++) {
            for ($j = $i + 1; $j < $len; $j++) {
                $str1 = (string)$nums[$i];
                $str2 = (string)$nums[$j];
                if (intval($str1.$str2) < intval($str2.$str1)) {
                    $tmp = $nums[$i];
                    $nums[$i] = $nums[$j];
                    $nums[$j] = $tmp;
                }
            }
        }
        $ret = '';
        foreach ($nums as $value) {
            $ret .= $value;
        }
        return $ret[0] == '0' ? '0' : $ret;
    }
}
```
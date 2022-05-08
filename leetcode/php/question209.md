```
给定一个含有 n 个正整数的数组和一个正整数 target 。
找出该数组中满足其和 ≥ target 的长度最小的 连续子数组 [numsl, numsl+1, ..., numsr-1, numsr] ，并返回其长度。如果不存在符合条件的子数组，返回 0 。

示例 1：
输入：target = 7, nums = [2,3,1,2,4,3]
输出：2
解释：子数组 [4,3] 是该条件下的长度最小的子数组。

示例 2：
输入：target = 4, nums = [1,4,4]
输出：1

示例 3：
输入：target = 11, nums = [1,1,1,1,1,1,1,1]
输出：0
```

```
class Solution {

    /**
     * @param Integer $target
     * @param Integer[] $nums
     * @return Integer
     */
    function minSubArrayLen($target, $nums) {
        $left = 0;
        $right = 0;
        $max = PHP_INT_MAX;
        $sum = 0;
        while ($right < count($nums)) {
            $sum += $nums[$right];
            while ($sum >= $target) {
                $max = min($max, $right - $left + 1);
                $sum -= $nums[$left];
                $left++;
            }
            $right++;
        }
        return $max == PHP_INT_MAX ? 0 : $max;
    }
}
```

```
class Solution {

    /**
     * @param Integer $target
     * @param Integer[] $nums
     * @return Integer
     */
    function minSubArrayLen($target, $nums) {
        $len = count($nums);
        $sum = $left = 0;
        $min = $len + 1;
        for ($i = 0; $i < $len; $i++) {
            $sum += $nums[$i];
            while ($sum >= $target) {
                $sum -= $nums[$left];
                $min = min($i - $left + 1, $min);
                $left++;
            }
        }

        return $min == $len + 1 ? 0 : $min;
    }
}
```
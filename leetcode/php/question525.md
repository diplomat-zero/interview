```
给定一个二进制数组 nums , 找到含有相同数量的 0 和 1 的最长连续子数组，并返回该子数组的长度。

示例 1:
输入: nums = [0,1]
输出: 2
说明: [0, 1] 是具有相同数量 0 和 1 的最长连续子数组。

示例 2:
输入: nums = [0,1,0]
输出: 2
说明: [0, 1] (或 [1, 0]) 是具有相同数量0和1的最长连续子数组。
 
提示：
1 <= nums.length <= 105
nums[i] 不是 0 就是 1
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function findMaxLength($nums) {
        $pre_sum[0] = 0;
        for ($i = 1; $i <= count($nums); $i++) {
            $val = $nums[$i - 1] == 0 ? -1 : 1;
            $pre_sum[$i] = $pre_sum[$i - 1] + $val;
        }

        $map = [];
        for ($m = 0; $m < count($pre_sum); $m++) {
            if (!isset($map[$pre_sum[$m]])) {
                $map[$pre_sum[$m]] = $m;
            }
        }

        $res = 0;
        for ($n = 1; $n < count($pre_sum); $n++) {
            if (isset($map[$pre_sum[$n]])) {
                $res = max($res, $n - $map[$pre_sum[$n]]);
            }
        }

        return $res;
    }
}
```
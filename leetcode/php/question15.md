```
给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有和为 0 且不重复的三元组。

注意：答案中不可以包含重复的三元组。

示例 1：
输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]

示例 2：
输入：nums = []
输出：[]

示例 3：
输入：nums = [0]
输出：[]
 
提示：
0 <= nums.length <= 3000
-105 <= nums[i] <= 105
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer[][]
     */
    function threeSum($nums) {
        $ret = [];
        $len = count($nums);
        for ($i = 0; $i < $len; $i++) {
            for ($j = 1; $j < $len; $j++) {
                if ($i == $j) {
                    continue;
                }
                $tmp = $nums;
                unset($tmp[$i], $tmp[$j]);
                $tmp = array_flip($tmp);
                $find = 0 - ($nums[$i] + $nums[$j]);
                if (isset($tmp[$find])) {
                    $tmp_arr = [$nums[$i], $nums[$j], $find];
                    sort($tmp_arr);
                    if (!in_array($tmp_arr, $ret)) {
                        $ret[] = $tmp_arr;
                    }
                }
            }
        }

        return $ret;
    }
}
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer[][]
     */
    function threeSum($nums) {
        $ret = [];

        sort($nums);
        if ($nums[0] > 0) {
            return [];
        }
        for ($i = 0; $i < count($nums); $i++) {
            if ($i > 0 && $nums[$i] == $nums[$i - 1]) {
                continue;
            }
            $left = $i + 1;
            $right = count($nums) - 1;
            while($left < $right) {
                $sum = $nums[$i] + $nums[$left] + $nums[$right];
                if ($sum == 0) {
                    $ret[] = [$nums[$i], $nums[$left], $nums[$right]];
                    while ($left < $right && $nums[$left] == $nums[$left + 1]) {
                        $left++;
                    }
                    while ($left < $right && $nums[$right] == $nums[$right - 1]){
                        $right--;
                    }
                    $left++;
                    $right--;
                } elseif ($sum > 0) {
                    $right--;
                } else {
                    $left++;
                }
            }
        }

        return $ret;
    }
}
```
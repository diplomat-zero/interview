```
给你一个整数数组 nums，请你将该数组升序排列。

示例 1：
输入：nums = [5,2,3,1]
输出：[1,2,3,5]

示例 2：
输入：nums = [5,1,1,2,0,0]
输出：[0,0,1,1,2,5]
 
提示：
1 <= nums.length <= 5 * 104
-5 * 104 <= nums[i] <= 5 * 104
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer[]
     */
    function sortArray($nums) {
        $this->split($nums, 0, count($nums) - 1);
        return $nums;
    }

    function split(&$arr, $left, $right) {
        if ($left >= $right) {
            return;
        }

        $mid = floor(($left + $right) / 2);
        $this->split($arr, $left, $mid);
        $this->split($arr, $mid + 1, $right);

        $this->merge($arr, $left, $mid, $right);
    }

    function merge(&$arr, $left, $mid, $right) {
        $tmp = [];
        $i = $left;
        $j = $mid + 1;

        while ($i <= $mid && $j <= $right) {
            if ($arr[$i] < $arr[$j]) {
                $tmp[] = $arr[$i];
                $i++;
            } else {
                $tmp[] = $arr[$j];
                $j++;
            } 
        }

        while ($i <= $mid) {
            $tmp[] = $arr[$i];
            $i++;
        }

        while ($j <= $right) {
            $tmp[] = $arr[$j];
            $j++;
        }

        for ($k = 0; $k < count($tmp); $k++) {
            $arr[$left + $k] = $tmp[$k];
        }
    }
}
```
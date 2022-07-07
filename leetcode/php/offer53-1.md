```
统计一个数字在排序数组中出现的次数。

 

示例 1:

输入: nums = [5,7,7,8,8,10], target = 8
输出: 2
示例 2:

输入: nums = [5,7,7,8,8,10], target = 6
输出: 0
 

提示：

0 <= nums.length <= 105
-109 <= nums[i] <= 109
nums 是一个非递减数组
-109 <= target <= 109
```

```

```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer
     */
    function search($nums, $target) {
        $left = 0;
        $right = count($nums) - 1;
        while ($left <= $right) {
            $mid = floor(($right - $left) / 2 + $left);
            if ($nums[$mid] == $target) {
                $start = $mid;
                $end = $mid;
                while ($nums[$start] == $target && $start >= $left) {
                    $start--;
                }
                while ($nums[$end] == $target && $end <= $right) {
                    $end++;
                }
                return $end - $start - 1;
            } elseif ($nums[$mid] > $target) {
                $right = $mid - 1;
            } else {
                $left = $mid + 1;
            }
        }
        return 0;
    }
}
```
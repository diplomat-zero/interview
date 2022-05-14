```
给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。
如果数组中不存在目标值 target，返回 [-1, -1]。

进阶：
你可以设计并实现时间复杂度为 O(log n) 的算法解决此问题吗？
 
示例 1：
输入：nums = [5,7,7,8,8,10], target = 8
输出：[3,4]

示例 2：
输入：nums = [5,7,7,8,8,10], target = 6
输出：[-1,-1]

示例 3：
输入：nums = [], target = 0
输出：[-1,-1]
 
提示：

0 <= nums.length <= 105
-109 <= nums[i] <= 109
nums 是一个非递减数组
-109 <= target <= 109
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[]
     */
    function searchRange($nums, $target) {
        $left = 0;
        $right = count($nums) - 1;

        while ($left <= $right) {
            $mid = floor(($right - $left) / 2 + $left);
            if ($nums[$mid] == $target) {
                $left1 = $mid;
                $right1 = $mid;
                while ($left1 >= 0 && $nums[$left1] == $target) {
                    $left1--;
                }
                while ($right1 < count($nums) && $nums[$right1] == $target) {
                    $right1++;
                }
                return [$left1 + 1, $right1 - 1];
            } else if ($nums[$mid] > $target) {
                $right = $mid - 1;
            } else {
                $left = $mid + 1;
            }
        }

        return [-1, -1];
    }
}
```

```
<?php
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[]
     */
    function searchRange($nums, $target) {
        return self::erfen($nums, $target, 0, count($nums) - 1);
    }

    function erfen($nums, $target, $left, $right) {
        if ($left > $right) {
            return [-1, -1];
        }
        $mid = $left;
        if ($nums[$mid] == $target) {
            $start = $end = $leftMid = $rightMid = $mid;
            while ($leftMid >= 0) {
                $leftMid--;
                if (isset($nums[$leftMid]) && $nums[$leftMid] == $nums[$mid]) {
                    $start = $leftMid;
                }
            }
            while ($rightMid <= count($nums) - 1) {
                $rightMid++;
                if (isset($nums[$rightMid]) && $nums[$rightMid] == $nums[$mid]) {
                    $end = $rightMid;
                }
            }
            return [$start, $end];
        } elseif ($nums[$mid] > $target) {
            return self::erfen($nums, $target, $left, $mid - 1);
        } elseif ($nums[$mid] < $target) {
            return self::erfen($nums, $target, $mid + 1, $right);
        }
    }
}
```
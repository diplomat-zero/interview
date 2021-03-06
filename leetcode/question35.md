```
给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。
你可以假设数组中无重复元素。

示例 1:
输入: [1,3,5,6], 5
输出: 2

示例 2:
输入: [1,3,5,6], 2
输出: 1

示例 3:
输入: [1,3,5,6], 7
输出: 4

示例 4:
输入: [1,3,5,6], 0
输出: 0
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer
     */
    function searchInsert($nums, $target) {
        return $this->erFen(0, count($nums) - 1, $nums, $target);
    }

    function erFen($left, $right, $nums, $target) {
        if ($left > $right) {
            return $right + 1;
        }
        $mid = intval(($left + $right) / 2);
        if ($nums[$mid] == $target) {
            return $mid;
        } elseif ($nums[$mid] > $target) {
            return $this->erFen($left, $right - 1,$nums, $target);
        } else {
            return $this->erFen($left + 1, $right, $nums, $target);
        }
    }
}
```
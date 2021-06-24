```
给你一个整数数组 nums ，数组中的元素 互不相同 。返回该数组所有可能的子集（幂集）。
解集 不能 包含重复的子集。你可以按 任意顺序 返回解集。

示例 1：
输入：nums = [1,2,3]
输出：[[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]

示例 2：
输入：nums = [0]
输出：[[],[0]]
 
提示：
1 <= nums.length <= 10
-10 <= nums[i] <= 10
nums 中的所有元素 互不相同
```

```
<?php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer[][]
     */
    function subsets($nums) {
        $result = [];
        self::dfs($nums, [], $result, 0);
        array_unshift($result, []);
        return $result;
    }

    function dfs($nums, $trace, &$result, $start) {
        if (!empty($trace)) {
            sort($trace);
            if (!in_array($trace, $result)) {
                $result[] = $trace;
            }
        }

        for ($i = $start; $i < count($nums); $i++) {
            if (!in_array($nums[$i], $trace) && count($trace) < count($nums)) {
                $trace[] = $nums[$i];
                self::dfs($nums, $trace, $result, $i + 1);
                array_pop($trace);
            }
        }
    }
}
```
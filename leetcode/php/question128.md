```
给定一个未排序的整数数组 nums ，找出数字连续的最长序列（不要求序列元素在原数组中连续）的长度。
进阶：你可以设计并实现时间复杂度为 O(n) 的解决方案吗？

示例 1：
输入：nums = [100,4,200,1,3,2]
输出：4
解释：最长数字连续序列是 [1, 2, 3, 4]。它的长度为 4。

示例 2：
输入：nums = [0,3,7,2,5,8,4,6,0,1]
输出：9
 
提示：
0 <= nums.length <= 104
-109 <= nums[i] <= 109
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function longestConsecutive($nums) {
        $max = PHP_INT_MIN;
        for ($i = 0; $i < count($nums); $i++) {
            $map[$nums[$i]] = $nums[$i];
        }

        foreach ($map as $key => $value) {
            $now_key = $key;
            if (isset($map[$now_key - 1])) {
                continue;
            }
            $start = 1;
            while (isset($map[$now_key + 1])) {
                $now_key++;
                $start++;
            }
            $max = max($max, $start);
        }
        return $max == PHP_INT_MIN ? 0 : $max;
    }
}
```

```
<?php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function longestConsecutive($nums) {
        if (empty($nums)) {
            return 0;
        } 
        sort($nums);

        $max = 0;
        $ret = 0;
        for ($i = 0; $i < count($nums); $i++) {
            if (($nums[$i] + 1) == $nums[$i + 1]) {
                $max++;
            } elseif ($nums[$i] == $nums[$i + 1]) {
                continue;
            } else {
                $ret = max($ret, $max);
                $max = 0;
            }
        }

        return max($ret, $max) + 1;
    }
}
```
```
给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。
请注意 ，必须在不复制数组的情况下原地对数组进行操作。

示例 1:
输入: nums = [0,1,0,3,12]
输出: [1,3,12,0,0]

示例 2:
输入: nums = [0]
输出: [0]
 
提示:
1 <= nums.length <= 104
-231 <= nums[i] <= 231 - 1
 
进阶：你能尽量减少完成的操作次数吗？
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return NULL
     */
    function moveZeroes(&$nums) {
        $p = $this->move($nums, 0);
        for (; $p < count($nums); $p++) {
            $nums[$p] = 0;
        }
    }

    function move(&$nums, $val) {
        $slow = 0;
        $fast = 0;
        while ($fast < count($nums)) {
            if ($nums[$fast] != $val) {
                $nums[$slow] = $nums[$fast];
                $slow++;
            }
            $fast++;
        }
        return $slow;
    }
}
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return NULL
     */
    function moveZeroes(&$nums) {
        $len = count($nums);
        $left = 0;
        $right = 0;
        while ($right < $len) {
            if ($nums[$right] != 0) {
                $tmp = $nums[$right];
                $nums[$right] = $nums[$left];
                $nums[$left] = $tmp;
                $left++;
            }
            $right++;
        }
        return $nums;
    }
}
```
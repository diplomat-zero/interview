```
给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

 

示例：

输入：nums = [-1,2,1,-4], target = 1
输出：2
解释：与 target 最接近的和是 2 (-1 + 2 + 1 = 2) 。
 

提示：

3 <= nums.length <= 10^3
-10^3 <= nums[i] <= 10^3
-10^4 <= target <= 10^4
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer
     */
    function threeSumClosest($nums, $target) {
        sort($nums);

        $res = $nums[0] + $nums[1] + $nums[count($nums) - 1];
        for ($i = 0; $i < count($nums); $i++) {
            $left = $i + 1;
            $right = count($nums) - 1;
            while ($left < $right) {
                $sum = $nums[$i] + $nums[$left] + $nums[$right];
                if (abs($sum - $target) < abs($res - $target)) {
                    $res = $sum;
                }
                if ($sum > $target) {
                    $right--;
                } elseif ($sum < $target) {
                    $left++;
                } else {
                    return $sum;
                }
            }
        }

        return $res;
    }
}
```
```
给你一个整型数组 nums ，在数组中找出由三个数组成的最大乘积，并输出这个乘积。

 

示例 1：

输入：nums = [1,2,3]
输出：6
示例 2：

输入：nums = [1,2,3,4]
输出：24
示例 3：

输入：nums = [-1,-2,-3]
输出：-6
 

提示：

3 <= nums.length <= 104
-1000 <= nums[i] <= 1000
```

```

```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function maximumProduct($nums) {
        $max1 = PHP_INT_MIN;
        $max2 = PHP_INT_MIN;
        $max3 = PHP_INT_MIN;
        $min1 = PHP_INT_MAX;
        $min2 = PHP_INT_MAX;
        for ($i = 0; $i < count($nums); $i++) {
            if ($nums[$i] < $min1) {
                $min2 = $min1;
                $min1 = $nums[$i];
            } else if ($nums[$i] < $min2) {
                $min2 = $nums[$i];
            }

            if ($nums[$i] > $max1) {
                $max3 = $max2;
                $max2 = $max1;
                $max1 = $nums[$i];
            } else if ($nums[$i] > $max2) {
                $max3 = $max2;
                $max2 = $nums[$i];
            } else if ($nums[$i] > $max3) {
                $max3 = $nums[$i];
            }
        }

        return max($max1 * $max2 * $max3, $max1 * $min1 * $min2);
    }
}
```
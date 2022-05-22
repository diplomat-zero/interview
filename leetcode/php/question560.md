```
给你一个整数数组 nums 和一个整数 k ，请你统计并返回 该数组中和为 k 的子数组的个数 。

示例 1：
输入：nums = [1,1,1], k = 2
输出：2

示例 2：
输入：nums = [1,2,3], k = 3
输出：2
 
提示：
1 <= nums.length <= 2 * 104
-1000 <= nums[i] <= 1000
-107 <= k <= 107
```

```
思路
前缀和+hash

遍历过程中，我们统计历史中每一个前缀和出现的个数，然后计算到i位置（含i）的前缀和presum减去目标k在历史上出现过几次，假如出现过m次，代表第i位以前（不含i）有m个连续子数组的和为presum−k，这m个和为presum−k的连续子数组，每一个都可以和presum组合成为presum - (presum - k) = k。
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $k
     * @return Integer
     */
    function subarraySum($nums, $k) {
        $res = 0;
        $pre_sum[0] = 0;
        $map[0] = 1;
        for ($i = 1; $i <= count($nums); $i++) {
            $pre_sum[$i] = $pre_sum[$i - 1] + $nums[$i - 1];
            $need = $pre_sum[$i] - $k;
            if (isset($map[$need])) {
                $res += $map[$need];
            }

            if (!isset($map[$pre_sum[$i]])) {
                $map[$pre_sum[$i]] = 1;
            } else {
                $map[$pre_sum[$i]] += 1;
            }
        }
        return $res;
    }
}
```
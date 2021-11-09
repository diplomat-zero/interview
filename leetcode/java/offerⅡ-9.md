```
给定一个正整数数组 nums和整数 k ，请找出该数组内乘积小于 k 的连续的子数组的个数。

示例 1:
输入: nums = [10,5,2,6], k = 100
输出: 8
解释: 8 个乘积小于 100 的子数组分别为: [10], [5], [2], [6], [10,5], [5,2], [2,6], [5,2,6]。
需要注意的是 [10,5,2] 并不是乘积小于100的子数组。

示例 2:
输入: nums = [1,2,3], k = 0
输出: 0
 
提示: 
1 <= nums.length <= 3 * 104
1 <= nums[i] <= 1000
0 <= k <= 106
```

```
class Solution {
    public int numSubarrayProductLessThanK(int[] nums, int k) {
        int left = 0;
        int right = 0;
        int sum = 1;
        int ret = 0;
        while (right < nums.length) {
            sum *= nums[right];
            while (sum >= k && left <= right) {
                sum /= nums[left];
                left++;
            }
            if (left <= right) {
                ret += right - left + 1;
            }
            right++;
        }

        return ret;
    }
}
```
```
给定一个整数数组和一个整数 k ，请找到该数组中和为 k 的连续子数组的个数。

示例 1 :
输入:nums = [1,1,1], k = 2
输出: 2
解释: 此题 [1,1] 与 [1,1] 为两种不同的情况

示例 2 :
输入:nums = [1,2,3], k = 3
输出: 2

提示:
1 <= nums.length <= 2 * 104
-1000 <= nums[i] <= 1000
-107 <= k <= 107
```

```
class Solution {
    public int subarraySum(int[] nums, int k) {
        int pre_sum = 0;
        int ret = 0;
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 1);
        for (int num: nums) {
            pre_sum += num;
            ret += map.getOrDefault(pre_sum - k,0);
            map.put(pre_sum, map.getOrDefault(pre_sum, 0) + 1);
        }

        return ret;
    }
}
```

```
https://blog.csdn.net/fgy_u/article/details/109349710
```
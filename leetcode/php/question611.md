```
给定一个包含非负整数的数组 nums ，返回其中可以组成三角形三条边的三元组个数。

示例 1:
输入: nums = [2,2,3,4]
输出: 3
解释:有效的组合是: 
2,3,4 (使用第一个 2)
2,3,4 (使用第二个 2)
2,2,3

示例 2:
输入: nums = [4,2,3,4]
输出: 4
 
提示:
1 <= nums.length <= 1000
0 <= nums[i] <= 1000
```

```
双指针

首先对数组排序。
固定最长的一条边，运用双指针扫描
如果 nums[l] + nums[r] > nums[i]，同时说明 nums[l + 1] + nums[r] > nums[i], ..., nums[r - 1] + nums[r] > nums[i]，满足的条件的有 r - l 种，r 左移进入下一轮。
如果 nums[l] + nums[r] <= nums[i]，l 右移进入下一轮。
枚举结束后，总和就是答案。
时间复杂度为 O(n^2)。
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function triangleNumber($nums) {
        sort($nums);
        $res = 0;
        for ($i = count($nums) - 1; $i >= 2; $i--) {
            $l = 0;
            $r = $i - 1;
            while ($l < $r) {
                if ($nums[$l] + $nums[$r] > $nums[$i]) {
                    $res += $r - $l;
                    $r--;
                } else {
                    $l++;
                }
            }
        }
        return $res;
    }
}
```
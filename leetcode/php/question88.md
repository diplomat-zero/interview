```
给你两个有序整数数组 nums1 和 nums2，请你将 nums2 合并到 nums1 中，使 nums1 成为一个有序数组。
初始化 nums1 和 nums2 的元素数量分别为 m 和 n 。你可以假设 nums1 的空间大小等于 m + n，这样它就有足够的空间保存来自 nums2 的元素。

示例 1：
输入：nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
输出：[1,2,2,3,5,6]

示例 2：
输入：nums1 = [1], m = 1, nums2 = [], n = 0
输出：[1]
 
提示：
nums1.length == m + n
nums2.length == n
0 <= m, n <= 200
1 <= m + n <= 200
-109 <= nums1[i], nums2[i] <= 10
```

```
class Solution {

    /**
     * @param Integer[] $nums1
     * @param Integer $m
     * @param Integer[] $nums2
     * @param Integer $n
     * @return NULL
     */
    function merge(&$nums1, $m, $nums2, $n) {
        $i = $j = 0;
        $tmp_num = [];
        while ($i < $m && $j < $n) {
            if ($nums1[$i] < $nums2[$j]) {
                $tmp_num[] = $nums1[$i];
                $i++;
            } else {
                $tmp_num[] = $nums2[$j];
                $j++;
            }
        }

        while ($i < $m) {
            $tmp_num[] = $nums1[$i];
            $i++;
        }

        while ($j < $n) {
            $tmp_num[] = $nums2[$j];
            $j++;
        }

        $nums1 = $tmp_num;
        return $nums1;
    }
}
```
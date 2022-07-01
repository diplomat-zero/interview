```
把符合下列属性的数组 arr 称为 山脉数组 ：

arr.length >= 3
存在下标 i（0 < i < arr.length - 1），满足
arr[0] < arr[1] < ... < arr[i - 1] < arr[i]
arr[i] > arr[i + 1] > ... > arr[arr.length - 1]
给出一个整数数组 arr，返回最长山脉子数组的长度。如果不存在山脉子数组，返回 0 。

 

示例 1：

输入：arr = [2,1,4,7,3,2,5]
输出：5
解释：最长的山脉子数组是 [1,4,7,3,2]，长度为 5。
示例 2：

输入：arr = [2,2,2]
输出：0
解释：不存在山脉子数组。
 

提示：

1 <= arr.length <= 104
0 <= arr[i] <= 104
 

进阶：

你可以仅用一趟扫描解决此问题吗？
你可以用 O(1) 空间解决此问题吗？
```

```

```

```
class Solution {

    /**
     * @param Integer[] $arr
     * @return Integer
     */
    function longestMountain($arr) {
        $dp1 = array_fill(0, count($arr), 1);
        $dp2 = array_fill(0, count($arr), 1);
        for ($i = 1; $i < count($arr); $i++) {
            if ($arr[$i] > $arr[$i - 1]) {
                $dp1[$i] = $dp1[$i - 1] + 1;
            }
        }
        for ($j = count($arr) - 1; $j > 0; $j--) {
            if ($arr[$j - 1] > $arr[$j]) {
                $dp2[$j - 1] = $dp2[$j] + 1;
            }
        }
        $res = PHP_INT_MIN;
        for ($p = 0; $p < count($arr); $p++) {
            if ($dp1[$p] > 1 && $dp2[$p] > 1) {
                $res = max($res, $dp1[$p] + $dp2[$p] - 1);
            }
        }
        return $res == PHP_INT_MIN ? 0 : $res;
    }
}
```
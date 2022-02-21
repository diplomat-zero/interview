```
输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）。
序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。

示例 1：
输入：target = 9
输出：[[2,3,4],[4,5]]

示例 2：
输入：target = 15
输出：[[1,2,3,4,5],[4,5,6],[7,8]]
 
限制：
1 <= target <= 10^5
```

```
class Solution {

    /**
     * @param Integer $target
     * @return Integer[][]
     */
    function findContinuousSequence($target) {
        $left = 1;
        $right = 2;
        $result = [];
        while ($left < $right) {
            $sum = ($left + $right) * ($right - $left + 1) / 2;
            if ($sum == $target) {
                $tmp = [];
                for ($i = $left; $i <= $right; $i++) {
                    $tmp[] = $i;
                }
                $result[] = $tmp;
                $left++;
            } elseif ($sum > $target) {
                $left++;
            } else {
                $right++;
            }
        }

        return $result;
    }
}
```
```
给你一个由 n 个整数组成的数组 nums ，和一个目标值 target 。请你找出并返回满足下述全部条件且不重复的四元组 [nums[a], nums[b], nums[c], nums[d]] （若两个四元组元素一一对应，则认为两个四元组重复）：

0 <= a, b, c, d < n
a、b、c 和 d 互不相同
nums[a] + nums[b] + nums[c] + nums[d] == target
你可以按 任意顺序 返回答案 。

 

示例 1：

输入：nums = [1,0,-1,0,-2,2], target = 0
输出：[[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
示例 2：

输入：nums = [2,2,2,2,2], target = 8
输出：[[2,2,2,2]]
 

提示：

1 <= nums.length <= 200
-109 <= nums[i] <= 109
-109 <= target <= 109
```

```

```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[][]
     */
    function fourSum($nums, $target) {
        $res = [];
        sort($nums);
        $len = count($nums);
        for ($i = 0; $i < $len - 3; $i++) {
            if ($i > 0 && $nums[$i] == $nums[$i - 1]) {
                continue;
            }
            for ($j = $i + 1; $j < $len - 2; $j++) {
                if ($j > $i + 1 && $nums[$j] == $nums[$j - 1]) {
                    continue;
                }
                $left = $j + 1;
                $right = $len - 1;
                while ($left < $right) {
                    $sum = $nums[$i] + $nums[$j] + $nums[$left] + $nums[$right];
                    if ($sum == $target) {
                        $tmp = [$nums[$i], $nums[$j], $nums[$left], $nums[$right]];
                        $res[] = $tmp;
                        while ($left < $right && $nums[$left] == $nums[$left + 1]) {
                            $left++;
                        }
                        $left++;
                        while ($left < $right && $nums[$right] == $nums[$right - 1]) {
                            $right--;
                        }
                        $right--;
                    } else if ($sum > $target) {
                        $right--;
                    } else {
                        $left++;
                    }
                }
            }
        }
        return $res;
    }
}
```
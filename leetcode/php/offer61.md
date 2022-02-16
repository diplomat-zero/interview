```
从若干副扑克牌中随机抽 5 张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，可以看成任意数字。A 不能视为 14。

示例 1:
输入: [1,2,3,4,5]
输出: True
 
示例 2:
输入: [0,0,1,2,5]
输出: True
 
限制：
数组长度为 5 
数组的数取值为 [0, 13] .
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return Boolean
     */
    function isStraight($nums) {
        sort($nums);
        $jokers = 0;
        for ($i = 0; $i < count($nums) - 1; $i++) {
            if ($nums[$i] == 0) {
                $jokers++;
            } elseif ($nums[$i] == $nums[$i + 1]) {
                return false;
            }
        }

        return $nums[4] - $nums[$jokers] < 5;
    }
}
```
```
给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。
candidates 中的数字可以无限制重复被选取。
说明：
所有数字（包括 target）都是正整数。
解集不能包含重复的组合。 

示例 1：
输入：candidates = [2,3,6,7], target = 7,
所求解集为：
[
  [7],
  [2,2,3]
]

示例 2：
输入：candidates = [2,3,5], target = 8,
所求解集为：
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
 
提示：
1 <= candidates.length <= 30
1 <= candidates[i] <= 200
candidate 中的每个元素都是独一无二的。
1 <= target <= 500
```

```
class Solution {

    /**
     * @param Integer[] $candidates
     * @param Integer $target
     * @return Integer[][]
     */
    function combinationSum($candidates, $target) {
        $trace = [];
        $result = [];
        $this->dfs($candidates, $target, 0, $trace, $result);
        return $result;
    }

    function dfs($candidates, $target, $start, $trace, &$result) {
        $sum = array_sum($trace);
        if ($sum == $target) {
            $result[] = $trace;
            return;
        }
        if ($sum > $target) {
            return;
        }

        for ($i = $start; $i < count($candidates); $i++) {
            $trace[] = $candidates[$i];
            $this->dfs($candidates, $target, $i, $trace, $result);
            array_pop($trace);
        }
    }
}
```

```
<?php
class Solution {

    /**
     * @param Integer[] $candidates
     * @param Integer $target
     * @return Integer[][]
     */
    function combinationSum($candidates, $target) {
        $result = [];
        self::dfs($candidates, [], $target, $result);
        return $result;
    }

    function dfs($num, $trace, $target, &$result) {
        if (!empty($trace)) {
            $sum = 0;
            foreach ($trace as $value) {
                $sum += $value;
            }
            if ($sum == $target) {
                sort($trace);
                if (!in_array($trace, $result)) {
                    $result[] = $trace;
                }
            }
        }

        for ($i = 0; $i < count($num); $i++) {
            if (array_sum($trace) < $target) {
                $trace[] = $num[$i];
                self::dfs($num, $trace, $target, $result);
                array_pop($trace);
            }
        }
    }
}
```
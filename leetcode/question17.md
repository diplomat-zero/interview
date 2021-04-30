```
给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。答案可以按 任意顺序 返回。
给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

2->abc
3->def
4->ghi
5->jkl
6->mn0
7->pqrs
8->tuv
9->wxyz

示例 1：
输入：digits = "23"
输出：["ad","ae","af","bd","be","bf","cd","ce","cf"]

示例 2：
输入：digits = ""
输出：[]

示例 3：
输入：digits = "2"
输出：["a","b","c"]
 
提示：
0 <= digits.length <= 4
digits[i] 是范围 ['2', '9'] 的一个数字。
```

```
<?php
class Solution {

    /**
     * @param String $digits
     * @return String[]
     */
    function letterCombinations($digits) {
        if (empty($digits)) {
            return [];
        }
        $map[2] = ['a','b','c'];
        $map[3] = ['d','e','f'];
        $map[4] = ['g','h','i'];
        $map[5] = ['j','k','l'];
        $map[6] = ['m','n','o'];
        $map[7] = ['p','q','r','s'];
        $map[8] = ['t','u','v'];
        $map[9] = ['w','x','y','z'];
        $result = [];
        self::trace(0, '', $digits, $result, $map);
        return $result;
    }

    function trace($index, $trace, $digits, &$result, $map) {
        if (strlen($digits) == $index) {
            $result[] = $trace;
            return;
        }

        $num = $map[$digits[$index]];
        for ($i = 0; $i < count($num); $i++) { 
            $trace .= $num[$i];
            self::trace($index + 1, $trace, $digits, $result, $map);
            $trace = substr($trace,0,strlen($trace)-1);
        }
    }
}
```
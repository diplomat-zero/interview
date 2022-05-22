```
给你一个字符串 s 、一个字符串 t 。返回 s 中涵盖 t 所有字符的最小子串。如果 s 中不存在涵盖 t 所有字符的子串，则返回空字符串 "" 。

注意：
对于 t 中重复字符，我们寻找的子字符串中该字符数量必须不少于 t 中该字符数量。
如果 s 中存在这样的子串，我们保证它是唯一的答案。
 
示例 1：
输入：s = "ADOBECODEBANC", t = "ABC"
输出："BANC"

示例 2：
输入：s = "a", t = "a"
输出："a"

示例 3:
输入: s = "a", t = "aa"
输出: ""
解释: t 中两个字符 'a' 均应包含在 s 的子串中，
因此没有符合条件的子字符串，返回空字符串。
 
提示：
1 <= s.length, t.length <= 105
s 和 t 由英文字母组成
 
进阶：你能设计一个在 o(n) 时间内解决此问题的算法吗？
```

```
思路
滑动窗口
模板
function slidingWindow($s, $t) {
    $window = [];
    $need = [];
    for ($i = 0; $i < strlen($t); $i++) {
        if (isset($need[$t[$i]])) {
            $need[$t[$i]]++;
        } else {
            $need[$t[$i]] = 1;
        }
    }
    
    $left = 0;
    $right = 0;
    $valid = 0; 
    while ($right < strlen($s)) {
        // c 是将移入窗口的字符
        $c = $s[$right];
        // 增大窗口
        $right++;
        // 进行窗口内数据的一系列更新
        ...

        /*** debug 输出的位置 ***/
        print_r($left . "\t" . $right . "\n");
        /********************/
        
        // 判断左侧窗口是否要收缩
        while (window needs shrink) {
            // d 是将移出窗口的字符
            $d = $s[$left];
            // 缩小窗口
            $left++;
            // 进行窗口内数据的一系列更新
            ...
        }
    }
}
```

```
class Solution {

    /**
     * @param String $s
     * @param String $t
     * @return String
     */
    function minWindow($s, $t) {
        $need = [];
        for ($i = 0; $i < strlen($t); $i++) {
            if (isset($need[$t[$i]])) {
                $need[$t[$i]]++;
            } else {
                $need[$t[$i]] = 1;
            }
        }
        $left = 0;
        $right = 0;
        $valid = 0;
        $window = [];
        $start = 0;
        $len = PHP_INT_MAX;
        while ($right < strlen($s)) {
            $c = $s[$right];
            $right++;
            if (isset($need[$c])) {
                $window[$c]++;
                if ($window[$c] == $need[$c]) {
                    $valid++;
                }
            }

            while ($valid == count($need)) {
                if ($right - $left < $len) {
                    $start = $left;
                    $len = $right - $left;
                }
                $char = $s[$left];
                $left++;
                if (isset($need[$char])) {
                    if ($need[$char] == $window[$char]) {
                        $valid--;
                    }
                    $window[$char]--;
                }
            }
        }

        return $len == PHP_INT_MAX ? '' : substr($s, $start, $len);
    }
}
```
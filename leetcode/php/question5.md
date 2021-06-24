```
给你一个字符串 s，找到 s 中最长的回文子串。

示例 1：
输入：s = "babad"
输出："bab"
解释："aba" 同样是符合题意的答案。

示例 2：
输入：s = "cbbd"
输出："bb"

示例 3：
输入：s = "a"
输出："a"

示例 4：
输入：s = "ac"
输出："a"
 
提示：
1 <= s.length <= 1000
s 仅由数字和英文字母（大写和/或小写）组成
```

```
<?php
class Solution {

    /**
     * @param String $s
     * @return String
     */
    function longestPalindrome($s) {
        $len = strlen($s);
        if ($len < 2) {
            return $s;
        }
        
        for ($m = 0; $m < $len; $m++) {
            $map[$m][$m] = true;
        }

        $start = 0;
        $max = 1;
        
        for ($r = 0; $r < $len; $r++) {
            for ($l = 0; $l < $r; $l++) {
                if ($s[$l] == $s[$r]) {
                    if ($r - $l < 3) {
                        $map[$l][$r] = true;
                    } else {
                        $map[$l][$r] = $map[$l + 1][$r - 1];
                    }
                } else {
                    $map[$l][$r] = false;
                }
                if ($map[$l][$r] && $r - $l + 1 > $max) {
                    $start = $l;
                    $max = $r - $l + 1;
                }
            }
        }

        return substr($s, $start, $max);
    }
}
```

```
根据官方提供思路写的 反而超时了
<?php
class Solution {

    /**
     * @param String $s
     * @return String
     */
    function longestPalindrome($s) {
        $len = strlen($s);
        if ($len < 2) {
            return $s;
        }
        
        for ($m = 0; $m < $len; $m++) {
            $map[$m][$m] = true;
        }

        $start = 0;
        $max = 1;
        for ($L = 2; $L <= $len; $L++) {
            for ($i = 0; $i < $len; $i++) {
                $j = $L + $i - 1;
                if ($j > $len - 1) {
                    break;
                }

                if ($s[$i] != $s[$j]) {
                    $map[$i][$j] = false;
                } else {
                    if ($j - $i < 3) {
                        $map[$i][$j] = true;
                    } else {
                        $map[$i][$j] = $map[$i + 1][$j - 1];
                    }
                }

                if ($map[$i][$j] && $L > $max) {
                    $max = $L;
                    $start = $i;
                }
            }
        }

        return substr($s, $start, $max);
    }
}
```
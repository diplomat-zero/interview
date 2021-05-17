```
给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。
说明：本题中，我们将空字符串定义为有效的回文串。

示例 1:
输入: "A man, a plan, a canal: Panama"
输出: true

示例 2:
输入: "race a car"
输出: false
```

```
<?php
class Solution {

    /**
     * @param String $s
     * @return Boolean
     */
    function isPalindrome($s) {
        $left = 0;
        $right = strlen($s) - 1;
        $arr = ['0','1','2','3','4','5','6','7','8','9','0','a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z'];
        while ($left < $right) {
            $left_char = strtolower($s[$left]);
            $right_char = strtolower($s[$right]);
            if (!in_array($left_char, $arr)) {
                $left++;
                continue;
            }
            if (!in_array($right_char, $arr)) {
                $right--;
                continue;
            }

            if ($left_char != $right_char) {
                return false;
            }
            $left++;
            $right--;
        }

        return true;
    }
}
```
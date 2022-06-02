```
给定一个非空字符串 s，最多删除一个字符。判断是否能成为回文字符串。

示例 1:
输入: s = "aba"
输出: true

示例 2:
输入: s = "abca"
输出: true
解释: 你可以删除c字符。

示例 3:
输入: s = "abc"
输出: false
 
提示:
1 <= s.length <= 105
s 由小写英文字母组成
```

```

```

```
class Solution {

    /**
     * @param String $s
     * @return Boolean
     */
    function validPalindrome($s) {
        $l = 0;
        $r = strlen($s) - 1;
        while ($l < $r) {
            if ($s[$l] == $s[$r]) {
                $l++;
                $r--;
            } else {
                return $this->valid($s, $l + 1, $r) || $this->valid($s, $l, $r - 1);
            }
        }
        return true;
    }

    function valid($s, $left, $right) {
        while ($left < $right) {
            if ($s[$left] != $s[$right]) {
                return false;
            }
            $left++;
            $right--;
        }
        return true;
    }
}
```
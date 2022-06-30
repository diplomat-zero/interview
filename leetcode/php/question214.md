```
给定一个字符串 s，你可以通过在字符串前面添加字符将其转换为回文串。找到并返回可以用这种方式转换的最短回文串。

 

示例 1：

输入：s = "aacecaaa"
输出："aaacecaaa"
示例 2：

输入：s = "abcd"
输出："dcbabcd"
 

提示：

0 <= s.length <= 5 * 104
s 仅由小写英文字母组成
```

```

```

```
class Solution {

    /**
     * @param String $s
     * @return String
     */
    function shortestPalindrome($s) {
        for ($i = strlen($s) - 1; $i >= 0; $i--) {
            if ($this->isPalindrome($s, 0, $i)) {
                break;
            }
        }
        $add = substr($s, $i + 1);
        return strrev($add) . $s;
    }

    function isPalindrome($s, $left, $right) {
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
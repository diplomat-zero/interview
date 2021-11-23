```
给定一个字符串 s ，验证 s 是否是 回文串 ，只考虑字母和数字字符，可以忽略字母的大小写。

本题中，将空字符串定义为有效的 回文串 。

示例 1:
输入: s = "A man, a plan, a canal: Panama"
输出: true
解释："amanaplanacanalpanama" 是回文串

示例 2:
输入: s = "race a car"
输出: false
解释："raceacar" 不是回文串

提示：
1 <= s.length <= 2 * 105
字符串 s 由 ASCII 字符组成
```

```
class Solution {
    public boolean isPalindrome(String s) {
        int len = s.length();
        int left = 0;
        int right = len - 1;
        while (left < right) {
            char left_char = Character.toLowerCase(s.charAt(left));
            char right_char = Character.toLowerCase(s.charAt(right));
            if (!isChar(left_char)) {
                left++;
                continue;
            }
            if (!isChar(right_char)) {
                right--;
                continue;
            }

            if (left_char != right_char) {
                return false;
            } else {
                left++;
                right--;
            }
        }

        return true;
    }

    public boolean isChar(char apl) {
        return (apl >= '0' && apl <= '9') || (apl >= 'a' && apl <= 'z');
    }
}
```
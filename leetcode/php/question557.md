```
给定一个字符串 s ，你需要反转字符串中每个单词的字符顺序，同时仍保留空格和单词的初始顺序。

示例 1：
输入：s = "Let's take LeetCode contest"
输出："s'teL ekat edoCteeL tsetnoc"

示例 2:
输入： s = "God Ding"
输出："doG gniD"
 
提示：
1 <= s.length <= 5 * 104
s 包含可打印的 ASCII 字符。
s 不包含任何开头或结尾空格。
s 里 至少 有一个词。
s 中的所有单词都用一个空格隔开。
```

```

```

```
class Solution {

    /**
     * @param String $s
     * @return String
     */
    function reverseWords($s) {
        $stack = [];
        $res = '';
        for ($i = 0; $i < strlen($s); $i++) {
            if ($s[$i] != ' ') {
                $stack[] = $s[$i];
            } else {
                while (!empty($stack)) {
                    $end = end($stack);
                    array_pop($stack);
                    $res .= $end;
                }
                $res .= ' ';
            }
        }
        while (!empty($stack)) {
            $end = end($stack);
            array_pop($stack);
            $res .= $end;
        }
        return $res;
    }
}
```
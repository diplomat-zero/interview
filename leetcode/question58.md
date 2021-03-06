```
给定一个仅包含大小写字母和空格 ' ' 的字符串 s，返回其最后一个单词的长度。如果字符串从左向右滚动显示，那么最后一个单词就是最后出现的单词。

如果不存在最后一个单词，请返回 0 。

说明：一个单词是指仅由字母组成、不包含任何空格字符的 最大子字符串。

 

示例:

输入: "Hello World"
输出: 5
```

```
class Solution {

    /**
     * @param String $s
     * @return Integer
     */
    function lengthOfLastWord($s) {
        $s = trim($s);
        $tmp = explode(' ',$s);
        $last = array_pop($tmp);
        return empty($last) ? 0 : strlen($last);
    }
}
```

```
class Solution {

    /**
     * @param String $s
     * @return Integer
     */
    function lengthOfLastWord($s) {
        $s = trim($s);
        $tmp = '';
        for ($i = 0; $i < strlen($s); $i++) {
            if ($s[$i] == ' ') {
                $tmp = '';
                continue;
            }
            $tmp .= $s[$i];
        }

        return empty($tmp) ? 0 : strlen($tmp);
    }
}
```
```
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串 s ，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
 

示例 1：

输入：s = "()"
输出：true
示例 2：

输入：s = "()[]{}"
输出：true
示例 3：

输入：s = "(]"
输出：false
示例 4：

输入：s = "([)]"
输出：false
示例 5：

输入：s = "{[]}"
输出：true
 

提示：

1 <= s.length <= 104
s 仅由括号 '()[]{}' 组成
```

```
class Solution {

    /**
     * @param String $s
     * @return Boolean
     */
    function isValid($s) {
        $ret = [];
        $in = ['(','[','{'];
        for ($i = 0; $i < strlen($s); $i++) {
            if (in_array($s[$i], $in)) {
                $ret[] = $s[$i];
            } else {
                $tmp = array_pop($ret);
                if (empty($tmp)) {
                    return false;
                }
                if (($tmp == '(' && $s[$i] == ')') || ($tmp == '[' && $s[$i] ==
                    ']') || ($tmp == '{' && $s[$i] == '}')) {
                    continue;
                }
                return false;
            }
        }
        return empty($ret);
    }
}
```
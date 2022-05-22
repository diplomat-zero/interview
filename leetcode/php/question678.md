```
给定一个只包含三种字符的字符串：（ ，） 和 *，写一个函数来检验这个字符串是否为有效字符串。有效字符串具有如下规则：
任何左括号 ( 必须有相应的右括号 )。
任何右括号 ) 必须有相应的左括号 ( 。
左括号 ( 必须在对应的右括号之前 )。
* 可以被视为单个右括号 ) ，或单个左括号 ( ，或一个空字符串。
一个空字符串也被视为有效字符串。

示例 1:
输入: "()"
输出: True

示例 2:
输入: "(*)"
输出: True

示例 3:
输入: "(*))"
输出: True

注意:
字符串大小将在 [1，100] 范围内。
```

```

```

```
class Solution {

    /**
     * @param String $s
     * @return Boolean
     */
    function checkValidString($s) {
        $left = [];
        $star = [];
        for ($i = 0; $i < strlen($s); $i++) {
            if ($s[$i] == '(') {
                $left[] = $i;
            } elseif ($s[$i] == '*') {
                $star[] = $i;
            } else {
                if (!empty($left)) {
                    array_pop($left);
                } elseif (!empty($star)) {
                    array_pop($star);
                } else {
                    return false;
                }
            }
        }
        if (empty($left) && empty($star)) {
            return true;
        } elseif (empty($left) && !empty($star)) {
            return true;
        } elseif (!empty($left) && empty($star)) {
            return false;
        } else {
            while (!empty($left)) {
                $left_top = array_pop($left);
                $star_top = array_pop($star);
                if ($star_top < $left_top) {
                    return false;
                }
            }
            return true;
        }
    }
}
```
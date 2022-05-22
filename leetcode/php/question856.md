```
给定一个平衡括号字符串 S，按下述规则计算该字符串的分数：
() 得 1 分。
AB 得 A + B 分，其中 A 和 B 是平衡括号字符串。
(A) 得 2 * A 分，其中 A 是平衡括号字符串。
 
示例 1：
输入： "()"
输出： 1

示例 2：
输入： "(())"
输出： 2

示例 3：
输入： "()()"
输出： 2

示例 4：
输入： "(()(()))"
输出： 6
 
提示：
S 是平衡括号字符串，且只含有 ( 和 ) 。
2 <= S.length <= 50
```

```

```

```
class Solution {

    /**
     * @param String $s
     * @return Integer
     */
    function scoreOfParentheses($s) {
        $stack = [];
        for ($i = 0; $i < strlen($s); $i++) {
            if ($s[$i] == '(') {
                $stack[] = $s[$i];
            } else {
                $end = end($stack);
                array_pop($stack);
                if ($end == '(') {
                    $stack[] = 1;
                } else {
                    $num = 0;
                    while ($end != '(') {
                        $num += $end;
                        $end = end($stack);
                        array_pop($stack);
                    }
                    $stack[] = $num * 2;
                }
            }
        }
        return array_sum($stack);
    }
}
```
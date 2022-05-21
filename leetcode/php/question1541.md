```
给你一个括号字符串 s ，它只包含字符 '(' 和 ')' 。一个括号字符串被称为平衡的当它满足：

任何左括号 '(' 必须对应两个连续的右括号 '))' 。
左括号 '(' 必须在对应的连续两个右括号 '))' 之前。
比方说 "())"， "())(())))" 和 "(())())))" 都是平衡的， ")()"， "()))" 和 "(()))" 都是不平衡的。

你可以在任意位置插入字符 '(' 和 ')' 使字符串平衡。

请你返回让 s 平衡的最少插入次数。

示例 1：
输入：s = "(()))"
输出：1
解释：第二个左括号有与之匹配的两个右括号，但是第一个左括号只有一个右括号。我们需要在字符串结尾额外增加一个 ')' 使字符串变成平衡字符串 "(())))" 。

示例 2：
输入：s = "())"
输出：0
解释：字符串已经平衡了。

示例 3：
输入：s = "))())("
输出：3
解释：添加 '(' 去匹配最开头的 '))' ，然后添加 '))' 去匹配最后一个 '(' 。

示例 4：
输入：s = "(((((("
输出：12
解释：添加 12 个 ')' 得到平衡字符串。

示例 5：
输入：s = ")))))))"
输出：5
解释：在字符串开头添加 4 个 '(' 并在结尾添加 1 个 ')' ，字符串变成平衡字符串 "(((())))))))" 。
 
提示：
1 <= s.length <= 10^5
s 只包含 '(' 和 ')' 。
```

```

```

```
class Solution {

    /**
     * @param String $s
     * @return Integer
     */
    function minInsertions($s) {
        $left_insert = 0;
        $right_need = 0;
        $right_insert = 0;
        for ($i = 0; $i < strlen($s); $i++) {
            if ($s[$i] == '(') {
                $right_need += 2;
                if ($right_need % 2 == 1) {
                    $right_insert++;
                    $right_need--;
                }
            } else {
                $right_need--;
                if ($right_need < 0) {
                    $left_insert++;
                    $right_need = 1;
                }
            }
        }
        return $left_insert + $right_need + $right_insert;
    }
}
```

```
class Solution {

    /**
     * @param String $s
     * @return Integer
     */
    function minInsertions($s) {
        if (strlen($s) == 0) {
            return 0;
        }
        $left = 0;
        $right = 0;
        for ($i = 0; $i < strlen($s); $i++) {
            if ($s[$i] == '(') {
                $right += 2;
                if ($right % 2 == 1) {
                    $left++;
                    $right--;
                }
            } else {
                $right--;
                if ($right < 0) {
                    $right = 1;
                    $left++;
                }
            }
        }
        return $left + $right;
    }
}
```
```
给定一个表示单词列表的字符串 s 。单词中的每个字母都有一个或多个选项。
如果有一个选项，则字母按原样表示。
如果有多个选项，则用大括号分隔选项。例如,  "{a,b,c}"  表示选项  ["a", "b", "c"]  。
例如，如果  s = "a{b,c}"  ，第一个字符总是 'a' ，但第二个字符可以是 'b' 或 'c' 。原来的列表是 ["ab", "ac"] 。
请你 按字典顺序 ，返回所有以这种方式形成的单词。

示例 1：
输入：s = "{a,b}c{d,e}f"
输出：["acdf","acef","bcdf","bcef"]

示例 2：
输入：s = "abcd"
输出：["abcd"]
 
提示：
1 <= S.length <= 50
s 由括号 '{}' , ',' 和小写英文字母组成。
s 保证是一个有效的输入。
没有嵌套的大括号。
在一对连续的左括号和右括号内的所有字符都是不同的
```

```

```

```
class Solution {

    /**
     * @param String $s
     * @return String[]
     */
    function expand($s) {
        $list = [];
        for ($i = 0; $i < strlen($s); $i++) {
            if ($s[$i] == '{') {
                $stack = '';
                $start = $i + 1;
                while ($s[$start] != '}') {
                    if ($s[$start] != ',') {
                        $stack .= $s[$start];
                    }
                    $start++;
                }
                $list[] = $stack;
                $i = $start;
            } else {
                $list[] = $s[$i];
            }
        }
        $result = [];
        $this->dfs($list, '', 0, $result);
        sort($result);
        return $result;
    }

    function dfs($list, $trace, $id, &$result) {
        if ($id >= count($list)) {
            $result[] = $trace;
            return;
        }
        for ($i = 0; $i < strlen($list[$id]); $i++) {
            $trace .= $list[$id][$i];
            $this->dfs($list, $trace, $id + 1, $result);
            $trace = substr($trace, 0, strlen($trace) - 1);
        }
    }
}
```
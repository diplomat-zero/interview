```
输入一个字符串，打印出该字符串中字符的所有排列。
你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。

示例:
输入：s = "abc"
输出：["abc","acb","bac","bca","cab","cba"]
 
限制：
1 <= s 的长度 <= 8
```

```
class Solution {

    /**
     * @param String $s
     * @return String[]
     */
    function permutation($s) {
        $result = []; 
        $trace = '';
        $dict = [];
        $this->dfs($s, $trace, $result, $dict);
        return $result;
    }

    function dfs($s, $trace, &$result, &$dict) {
        if (strlen($s) == strlen($trace)) {
            if (!in_array($trace, $result)) {
                $result[] = $trace;
            }
            return;
        }

        for ($i = 0; $i < strlen($s); $i++) {
            if (!isset($dict[$i])) {
                $dict[$i] = 1;
                $trace .= $s[$i];
                $this->dfs($s, $trace, $result, $dict);
                $trace = substr($trace, 0, -1);
                unset($dict[$i]);
            }
        }
    }
}
```
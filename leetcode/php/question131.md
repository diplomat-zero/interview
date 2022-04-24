```
给你一个字符串 s，请你将 s 分割成一些子串，使每个子串都是 回文串 。返回 s 所有可能的分割方案。
回文串 是正着读和反着读都一样的字符串。

示例 1：
输入：s = "aab"
输出：[["a","a","b"],["aa","b"]]

示例 2：
输入：s = "a"
输出：[["a"]]
 
提示：
1 <= s.length <= 16
s 仅由小写英文字母组成
```

```
class Solution {

    /**
     * @param String $s
     * @return String[][]
     */
    function partition($s) {
        $dp = [];
        for ($right = 0; $right < strlen($s); $right++) {
            for ($left = 0; $left <= $right; $left++) {
                if ($s[$right] == $s[$left] && ($right - $left <= 2 || $dp[$left+ 1][$right - 1])) {
                    $dp[$left][$right] = true;
                }
            }
        }
        $trace = [];
        $result = [];
        $this->dfs($s, 0, $trace, $result, $dp);
        return $result;
    }

    function dfs($s, $start, &$trace, &$result, $dp)
    {
        if ($start == strlen($s)) {
            $result[] = $trace;
            return;
        }
        for ($i = $start; $i < strlen($s); $i++) {
            if ($dp[$start][$i]) {
                $trace[] = substr($s, $start, $i - $start + 1);
                $this->dfs($s, $i + 1, $trace, $result, $dp);
                array_pop($trace);
            }
        }
    }
}
```
```
有效 IP 地址 正好由四个整数（每个整数位于 0 到 255 之间组成，且不能含有前导 0），整数之间用 '.' 分隔。

例如："0.1.2.201" 和 "192.168.1.1" 是 有效 IP 地址，但是 "0.011.255.245"、"192.168.1.312" 和 "192.168@1.1" 是 无效 IP 地址。
给定一个只包含数字的字符串 s ，用以表示一个 IP 地址，返回所有可能的有效 IP 地址，这些地址可以通过在 s 中插入 '.' 来形成。你 不能 重新排序或删除 s 中的任何数字。你可以按 任何 顺序返回答案。

示例 1：
输入：s = "25525511135"
输出：["255.255.11.135","255.255.111.35"]

示例 2：
输入：s = "0000"
输出：["0.0.0.0"]

示例 3：
输入：s = "101023"
输出：["1.0.10.23","1.0.102.3","10.1.0.23","10.10.2.3","101.0.2.3"]
 
提示：
1 <= s.length <= 20
s 仅由数字组成
```

```
思路
回溯
```

```
class Solution {

    /**
     * @param String $s
     * @return String[]
     */
    function restoreIpAddresses($s) {
        $trace = [];
        $result = [];
        $split = 0;
        $map[0] = 12;
        $map[1] = 9;
        $map[2] = 6;
        $map[3] = 3;
        $this->dfs($s, 0, $split, $trace, $result, $map);
        return array_unique($result);
    }

    function dfs($s, $start, $split, $trace, &$result, $map) {
        $len = strlen(substr($s, $start));
        if ($map[$split] < $len) {
            return;
        }
        if (count($trace) == 4) {
            $res = implode('.', $trace);
            $result[] = $res;
            return;
        }

        for ($i = 1; $i <= 3; $i++) {
            $tmp = substr($s, $start, $i);
            if ($this->can($tmp)) {
                $trace[] = $tmp;
                $split++;
                $this->dfs($s, $start + $i, $split, $trace, $result, $map);
                array_pop($trace);
                $split--;
            }
        }
    }

    function can($tmp) {
        $numLen = strlen($tmp);
        $numStr = $tmp;
        if ($numLen > 3 || $numLen < 1) {
            return false;
        }
        if ($numStr > 255) {
            return false;
        }
        if ($numLen > 1 && $numStr[0] == '0') {
            return false;
        }

        return true;
    }
}
```
```
给你一个由若干括号和字母组成的字符串 s ，删除最小数量的无效括号，使得输入的字符串有效。
返回所有可能的结果。答案可以按 任意顺序 返回。

示例 1：
输入：s = "()())()"
输出：["(())()","()()()"]

示例 2：
输入：s = "(a)())()"
输出：["(a())()","(a)()()"]

示例 3：
输入：s = ")("
输出：[""]
 
提示：
1 <= s.length <= 25
s 由小写英文字母以及括号 '(' 和 ')' 组成
s 中至多含 20 个括号
```

```
题目让我们删除括号使得剩下的括号匹配，要求我们删除最少的括号数，并且要求得到所有的结果。我们可以使用回溯算法，尝试遍历所有可能的去掉非法括号的方案。

首先我们利用括号匹配的规则求出该字符串 s 中最少需要去掉的左括号的数目 lremove 和右括号的数目 rremove，然后我们尝试在原字符串 s 中去掉 lremove 个左括号和 rremove 个右括号，然后检测剩余的字符串是否合法匹配，如果合法匹配则我们则认为该字符串为可能的结果，我们利用回溯算法来尝试搜索所有可能的去除括号的方案。

在进行回溯时可以利用以下的剪枝技巧来增加搜索的效率：

我们从字符串中每去掉一个括号，则更新 lremove 或者 rremove，当我们发现剩余未尝试的字符串的长度小于 lremove+rremove 时，则停止本次搜索。
当 lremove 和 rremove 同时为 0 时，则我们检测当前的字符串是否合法匹配，如果合法匹配则我们将其记录下来。
由于记录的字符串可能存在重复，因此需要对重复的结果进行去重，去重的办法有如下两种：

利用哈希表对最终生成的字符串去重。
我们在每次进行搜索时，如果遇到连续相同的括号我们只需要搜索一次即可，比如当前遇到的字符串为 "(((())"，去掉前四个左括号中的任意一个，生成的字符串是一样的，均为 "((())"，因此我们在尝试搜索时，只需去掉一个左括号进行下一轮搜索，不需要将前四个左括号都尝试一遍。
```

```
class Solution {

    /**
     * @param String $s
     * @return String[]
     */
    function removeInvalidParentheses($s) {
        $left = 0;
        $right = 0;
        for ($i = 0; $i < strlen($s); $i++) {
            if ($s[$i] == '(') {
                $left++;
            } elseif ($s[$i] == ')') {
                if ($left == 0) {
                    $right++;
                } else {
                    $left--;
                }
            }
        }
        if ($left == 0 && $right == 0) {
            return [$s];
        }
        $result = [];
        $this->dfs(0, $left, $right, $s,$result);
        return empty($result) ? [""] : $result;
    }

    function dfs($start, $left, $right, $s, &$result) {
        if ($left == 0 && $right == 0) {
            if ($this->isValid($s)) {
                $result[] = $s;
                return;
            }
        }

        for ($i = $start; $i < strlen($s); $i++) {
            if ($i > $start && $s[$i] == $s[$i - 1]) {
                continue;
            }
            if ($left + $right > strlen($s) - $i) {
                return;
            }
            if ($left > 0 && $s[$i] == '(') {
                $str = substr($s, 0, $i) . substr($s, $i + 1);
                $this->dfs($i, $left - 1, $right, $str,$result);
                $str = $s;
            }
            if ($right > 0 && $s[$i] == ')') {
                $str = substr($s, 0, $i) . substr($s, $i + 1);
                $this->dfs($i, $left, $right -  1, $str,$result);
                $str = $s;
            }
        }
    }

    function isValid($str) {
        $left = 0;
        for ($i = 0; $i < strlen($str); $i++) {
            if ($str[$i] == '(') {
                $left++;
            } elseif ($str[$i] == ')') {
                $left--;
                if ($left < 0) {
                    return false;
                }
            }
        }
        return $left == 0;
    }
}
```
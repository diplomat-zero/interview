```
给你两个单词 word1 和 word2，请你计算出将 word1 转换成 word2 所使用的最少操作数 。

你可以对一个单词进行如下三种操作：

插入一个字符
删除一个字符
替换一个字符
 

示例 1：
输入：word1 = "horse", word2 = "ros"
输出：3
解释：
horse -> rorse (将 'h' 替换为 'r')
rorse -> rose (删除 'r')
rose -> ros (删除 'e')

示例 2：
输入：word1 = "intention", word2 = "execution"
输出：5
解释：
intention -> inention (删除 't')
inention -> enention (将 'i' 替换为 'e')
enention -> exention (将 'n' 替换为 'x')
exention -> exection (将 'n' 替换为 'c')
exection -> execution (插入 'u')
 

提示：
0 <= word1.length, word2.length <= 500
word1 和 word2 由小写英文字母组成
```

```
class Solution {

    /**
     * @param String $word1
     * @param String $word2
     * @return Integer
     */
    function minDistance($word1, $word2) {
        if ($word1 == $word2) {
            return 0;
        }
        $dp = [];
        $m = strlen($word1);
        $n = strlen($word2);
        for ($i = 1; $i <= $m; $i++) {
            $dp[$i][0] = $i;
        }
        for ($j = 1; $j <= $n; $j++) {
            $dp[0][$j] = $j;
        }

        for ($p = 1; $p <= $m; $p++) {
            for ($q = 1; $q <= $n; $q++) {
                if ($word1[$p - 1] == $word2[$q - 1]) {
                    $dp[$p][$q] = $dp[$p - 1][$q - 1];
                } else {
                    $dp[$p][$q] = min($dp[$p - 1][$q - 1] + 1, $dp[$p - 1][$q] + 1, $dp[$p][$q - 1] + 1);
                }
            }
        }
        return $dp[$m][$n];
    }
}
```
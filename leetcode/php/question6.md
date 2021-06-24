```
将一个给定字符串 s 根据给定的行数 numRows ，以从上往下、从左到右进行 Z 字形排列。

比如输入字符串为 "PAYPALISHIRING" 行数为 3 时，排列如下：

P   A   H   N
A P L S I I G
Y   I   R
之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："PAHNAPLSIIGYIR"。

请你实现这个将字符串进行指定行数变换的函数：

string convert(string s, int numRows);
 

示例 1：
输入：s = "PAYPALISHIRING", numRows = 3
输出："PAHNAPLSIIGYIR"

示例 2：
输入：s = "PAYPALISHIRING", numRows = 4
输出："PINALSIGYAHRPI"
解释：
 0 1 2 3 4 5 6 X
0P     I     N
1A   L S   I G
2Y A   H R
3P     I
Y

示例 3：
输入：s = "A", numRows = 1
输出："A"

提示：

1 <= s.length <= 1000
s 由英文字母（小写和大写）、',' 和 '.' 组成
1 <= numRows <= 1000
```

```
class Solution {

    /**
     * @param String $s
     * @param Integer $numRows
     * @return String
     */
    function convert($s, $numRows) {
        if ($numRows == 1) {
            return $s;
        }

        $result = '';
        $tmp = [];
        $tmpX = $tmpY = 0;
        $a = true;
        for ($i = 0; $i < strlen($s); $i++) {
            $tmp[$tmpX][$tmpY] = $s[$i];
            if (($tmpY < $numRows - 1) && $a) {
                $tmpY = $tmpY + 1;
            } else {
                $a = false;
                $tmpY = $tmpY - 1;
                $tmpX = $tmpX + 1;
                if ($tmpY == 0) {
                    $a = true;
                }
            }
        }

        for($j = 0; $j < $numRows; $j++) {
            for ($i = 0; $i <= $tmpX; $i++) {
                isset($tmp[$i][$j]) && $result .= $tmp[$i][$j];
            }
        }
        return $result;
    }
}
```
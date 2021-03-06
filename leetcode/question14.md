```
编写一个函数来查找字符串数组中的最长公共前缀。
如果不存在公共前缀，返回空字符串 ""。

示例 1：
输入：strs = ["flower","flow","flight"]
输出："fl"

示例 2：
输入：strs = ["dog","racecar","car"]
输出：""
解释：输入不存在公共前缀。
 
提示：
0 <= strs.length <= 200
0 <= strs[i].length <= 200
strs[i] 仅由小写英文字母组成
```

```
class Solution {

    /**
     * @param String[] $strs
     * @return String
     */
    function longestCommonPrefix($strs) {
        $len = count($strs);

        if ($len == 1) {
            return $strs[0];
        }
        $pre = $this->findPre($strs[0], $strs[1]);
        if (empty($pre)) {
            return "";
        }

        for ($i = 2; $i < $len; $i++) {
            $pre = $this->findPre($pre, $strs[$i]);
            if (empty($pre)) {
                return "";
            }
        }

        return $pre;
    }

    function findPre($str1, $str2) {
        $len1 = strlen($str1);
        $len2 = strlen($str2);
        $i = $j = 0;
        $pre = '';
        while ($i < $len1 && $j < $len2) {
            if ($str1[$i] == $str2[$j]) {
                $pre .= $str1[$i];
                $i++;
                $j++;
            } else {
                break;
            }
        }

        return $pre;
    }
}
```
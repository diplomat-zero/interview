```
给你一个字符串数组 words ，请你找出所有在 words 的每个字符串中都出现的共用字符（ 包括重复字符），并以数组形式返回。你可以按 任意顺序 返回答案。
 
示例 1：
输入：words = ["bella","label","roller"]
输出：["e","l","l"]

示例 2：
输入：words = ["cool","lock","cook"]
输出：["c","o"]
 
提示：
1 <= words.length <= 100
1 <= words[i].length <= 100
words[i] 由小写英文字母组成
```

```

```

```
class Solution {

    /**
     * @param String[] $words
     * @return String[]
     */
    function commonChars($words) {
        $map = [
            'a' => 0,
            'b' => 0,
            'c' => 0,
            'd' => 0,
            'e' => 0,
            'f' => 0,
            'g' => 0,
            'h' => 0,
            'i' => 0,
            'j' => 0,
            'k' => 0,
            'l' => 0,
            'm' => 0,
            'n' => 0,
            'o' => 0,
            'p' => 0,
            'q' => 0,
            'r' => 0,
            's' => 0,
            't' => 0,
            'u' => 0,
            'v' => 0,
            'w' => 0,
            'x' => 0,
            'y' => 0,
            'z' => 0,
        ];
        for ($j = 0; $j < count($words); $j++) {
            $hash = [];
            for ($i = 0; $i < strlen($words[$j]); $i++) {
                if (isset($hash[$words[$j][$i]])) {
                    $hash[$words[$j][$i]]++;
                } else {
                    $hash[$words[$j][$i]] = 1;
                }
            }
            foreach ($map as $key => $value) {
                if ($j == 0) {
                    $map[$key] = $hash[$key];
                } else {
                    $map[$key] = min($map[$key], $hash[$key]);
                }
            }
        }
        $ret = [];
        foreach ($map as $key1 => $value1) {
            if (!empty($value1)) {
                for ($m = 0; $m < $value1; $m++) {
                    $ret[] = $key1;
                }
            }
        }
        return $ret;
    }
}
```
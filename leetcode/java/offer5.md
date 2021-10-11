```
请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

示例 1：
输入：s = "We are happy."
输出："We%20are%20happy."
 
限制
0 <= s 的长度 <= 10000
```

```
class Solution {
    public String replaceSpace(String s) {

        StringBuilder ret = new StringBuilder();

        for (int i = 0; i < s.length(); i++) {
            char apl = s.charAt(i);
            if (apl == ' ') {
                ret.append("%20");
            } else {
                ret.append(apl);
            }
        }

        return ret.toString();
    }
}
```
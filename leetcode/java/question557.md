```
给定一个字符串，你需要反转字符串中每个单词的字符顺序，同时仍保留空格和单词的初始顺序。

示例：
输入："Let's take LeetCode contest"
输出："s'teL ekat edoCteeL tsetnoc"
 
提示：
在字符串中，每个单词由单个空格分隔，并且字符串中不会有任何额外的空格。
```

```
class Solution {
    public String reverseWords(String s) {
        StringBuilder tmp = new StringBuilder();
        StringBuilder ret = new StringBuilder();
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == ' ') {
                ret.append(tmp);
                ret.append(s.charAt(i));
                tmp.setLength(0);
            } else {
                tmp.insert(0, s.charAt(i));
            }
        }

        if (tmp.length() > 0) {
            ret.append(tmp);
        }

        return ret.toString();
    }
}
```
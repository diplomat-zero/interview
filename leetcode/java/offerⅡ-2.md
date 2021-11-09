```
给定两个 01 字符串 a 和 b ，请计算它们的和，并以二进制字符串的形式输出。
输入为 非空 字符串且只包含数字 1 和 0。

示例 1:
输入: a = "11", b = "10"
输出: "101"

示例 2:
输入: a = "1010", b = "1011"
输出: "10101"
 
提示：
每个字符串仅由字符 '0' 或 '1' 组成。
1 <= a.length, b.length <= 10^4
字符串如果不是 "0" ，就都不含前导零。
```

```
class Solution {
    public String addBinary(String a, String b) {
        int a_len = a.length();
        int b_len = b.length();
        int jin = 0;
        StringBuilder res = new StringBuilder();
        while (a_len > 0 || b_len > 0 || jin != 0) {
            int tmp_a = a_len > 0 ? a.charAt(a_len - 1) - '0' : 0;
            int tmp_b = b_len > 0 ? b.charAt(b_len - 1) - '0' : 0;

            int tmp = tmp_a + tmp_b + jin;
            if (tmp >= 2) {
                jin = 1;
                tmp = tmp - 2;
            } else {
                jin = 0;
            }
            res.append(tmp);
            a_len--;
            b_len--;
        }

        return res.reverse().toString();
    }
}
```
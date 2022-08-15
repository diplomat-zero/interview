```
给你一个字符串 s 、一个字符串 t 。返回 s 中涵盖 t 所有字符的最小子串。如果 s 中不存在涵盖 t 所有字符的子串，则返回空字符串 "" 。

 

注意：

对于 t 中重复字符，我们寻找的子字符串中该字符数量必须不少于 t 中该字符数量。
如果 s 中存在这样的子串，我们保证它是唯一的答案。
 

示例 1：

输入：s = "ADOBECODEBANC", t = "ABC"
输出："BANC"
示例 2：

输入：s = "a", t = "a"
输出："a"
示例 3:

输入: s = "a", t = "aa"
输出: ""
解释: t 中两个字符 'a' 均应包含在 s 的子串中，
因此没有符合条件的子字符串，返回空字符串。
 

提示：

1 <= s.length, t.length <= 105
s 和 t 由英文字母组成
 

进阶：你能设计一个在 o(n) 时间内解决此问题的算法吗？
```

```

```

```
class Solution {
    public String minWindow(String s, String t) {
        int left = 0;
        int right = 0;
        int valid = 0;

        Map<Character, Integer> need = new HashMap<Character, Integer>();
        for (int i = 0; i < t.length(); i++) {
            char t_c = t.charAt(i);
            if (need.containsKey(t_c)) {
                need.put(t_c, need.get(t_c) + 1);
            } else {
                need.put(t_c, 1);
            }
        }

        Map<Character, Integer> windows = new HashMap<Character, Integer>();

        int start = 0;
        int len = Integer.MAX_VALUE;
        while (right < s.length()) {
            char right_char = s.charAt(right);
            right++;
            if (need.containsKey(right_char)) {
                if (windows.containsKey(right_char)) {
                    windows.put(right_char, windows.get(right_char) + 1);
                } else {
                    windows.put(right_char, 1);
                }
                if (windows.get(right_char).equals(need.get(right_char))) {
                    valid++;
                }
            }

            while (valid == need.size()) {
                if (right - left < len) {
                    len = right - left;
                    start = left;
                }
                char left_char = s.charAt(left);
                left++;
                if (need.containsKey(left_char)) {
                    if (windows.get(left_char).equals(need.get(left_char))) {
                        valid--;
                    }
                    windows.put(left_char, windows.get(left_char) - 1);
                }
            }
        }

        return len == Integer.MAX_VALUE ? "" : s.substring(start, start + len);
    }
}
```
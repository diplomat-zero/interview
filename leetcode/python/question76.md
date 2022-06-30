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
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        dict_map = {}
        for i in range(len(t)):
            if t[i] in dict_map:
                dict_map[t[i]] += 1
            else:
                dict_map[t[i]] = 1
        
        left = 0
        right = 0
        window = {}
        start = 0
        length = len(s) * 2
        valid = 0
        while right < len(s):
            char = s[right]
            right += 1
            if char in dict_map:
                if char in window:
                    window[char] += 1
                else:
                    window[char] = 1
                if window[char] == dict_map[char]:
                    valid += 1
            while valid == len(dict_map):
                if right - left < length:
                    start = left
                    length = right - left
                left_char = s[left]
                left += 1
                if left_char in dict_map:
                    if dict_map[left_char] == window[left_char]:
                        valid -= 1
                    window[left_char] -= 1
        
        if length == len(s) * 2:
            return ''
        else:
            return s[start:start+length]
```
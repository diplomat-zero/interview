```
请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

 

示例 1:

输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
示例 2:

输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
示例 3:

输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
 

提示：

s.length <= 40000
```

```

```

```
func lengthOfLongestSubstring(s string) int {
    left := 0
    right := 0
    res := 0
    s_map := make(map[string]int)
    for right < len(s) {
        right_char := string(s[right])
        right++
        s_map[right_char]++
        for s_map[right_char] > 1 {
            left_char := string(s[left])
            left++
            s_map[left_char]--
        }
        if right - left > res {
            res = right - left
        }
    }
    return res
}
```
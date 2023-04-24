```
给定两个字符串 s 和 p，找到 s 中所有 p 的 异位词 的子串，返回这些子串的起始索引。不考虑答案输出的顺序。

异位词 指由相同字母重排列形成的字符串（包括相同的字符串）。

 

示例 1:

输入: s = "cbaebabacd", p = "abc"
输出: [0,6]
解释:
起始索引等于 0 的子串是 "cba", 它是 "abc" 的异位词。
起始索引等于 6 的子串是 "bac", 它是 "abc" 的异位词。
 示例 2:

输入: s = "abab", p = "ab"
输出: [0,1,2]
解释:
起始索引等于 0 的子串是 "ab", 它是 "ab" 的异位词。
起始索引等于 1 的子串是 "ba", 它是 "ab" 的异位词。
起始索引等于 2 的子串是 "ab", 它是 "ab" 的异位词。
 

提示:

1 <= s.length, p.length <= 3 * 104
s 和 p 仅包含小写字母
```

```

```

```
func findAnagrams(s string, p string) []int {
    res := make([]int, 0)
    p_map := make(map[string]int)
    for _,value := range p {
        p_map[string(value)]++
    }
    left := 0
    right := 0
    valid := 0
    s_map := make(map[string]int)
    for right < len(s) {
        right_char := string(s[right])
        right++
        if _,ok := p_map[right_char];ok {
            s_map[right_char]++
            if s_map[right_char] == p_map[right_char] {
                valid++
            }
        }
        for right - left >= len(p) {
            if valid == len(p_map) {
                res = append(res, left)
            }
            left_char := string(s[left])
            left++
            if _,ok := p_map[left_char]; ok {
                if s_map[left_char] == p_map[left_char] {
                    valid--
                }
                s_map[left_char]--
            }
        }
    }
    return res
}
```
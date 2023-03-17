```
给你两个字符串 s1 和 s2 ，写一个函数来判断 s2 是否包含 s1 的排列。如果是，返回 true ；否则，返回 false 。

换句话说，s1 的排列之一是 s2 的 子串 。

 

示例 1：

输入：s1 = "ab" s2 = "eidbaooo"
输出：true
解释：s2 包含 s1 的排列之一 ("ba").
示例 2：

输入：s1= "ab" s2 = "eidboaoo"
输出：false
 

提示：

1 <= s1.length, s2.length <= 104
s1 和 s2 仅包含小写字母
```

```

```

```
func checkInclusion(s1 string, s2 string) bool {
    s1_map := make(map[string]int)
    for _,value := range s1 {
        s1_map[string(value)]++
    }
    count := 0
    s2_map := make(map[string]int)
    left := 0
    right := 0
    for right < len(s2) {
        right_char := string(s2[right])
        right++
        if _,ok := s1_map[right_char]; ok {
            s2_map[right_char]++
            if s2_map[right_char] == s1_map[right_char] {
                count++
            }
        }
        for count == len(s1_map) {
            if right - left == len(s1) {
                return true
            }
            left_char := string(s2[left])
            left++
            if _,ok := s2_map[left_char]; ok {
                s2_map[left_char]--
                if s2_map[left_char] < s1_map[left_char] {
                    count--
                }
            }
        }
    }
    return false
}
```
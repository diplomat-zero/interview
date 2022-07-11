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
func minWindow(s string, t string) string {
    t_map := make(map[string]int)

	for i := 0; i < len(t); i++ {
		char := string(t[i])
		_,ok := t_map[char]
		if ok {
			t_map[char]++
		} else {
			t_map[char] = 1
		}
	}

	left := 0
	right := 0
	valid := 0
	s_map := make(map[string]int)
	start_left := 0
	end_left := 0
	length := math.MaxInt

	for right < len(s) {
		right_char := string(s[right])
		right++
		_,ok := t_map[right_char]
		if ok {
			s_map[right_char]++
		}
		if s_map[right_char] > 0 && t_map[right_char] > 0 && s_map[right_char] == t_map[right_char] {
			valid++
		}

		for valid == len(t_map) {
			if right - left < length {
				end_left = right
				start_left = left
				length = end_left - start_left
			}
			left_char := string(s[left])
			left++
			_,ok := t_map[left_char]
			if ok {
				if t_map[left_char] == s_map[left_char] {
					valid--
				}
				s_map[left_char]--
			}
		}
	} 
    return s[start_left:end_left]
}
```
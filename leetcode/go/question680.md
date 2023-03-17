```
给你一个字符串 s，最多 可以从中删除一个字符。

请你判断 s 是否能成为回文字符串：如果能，返回 true ；否则，返回 false 。

 

示例 1：

输入：s = "aba"
输出：true
示例 2：

输入：s = "abca"
输出：true
解释：你可以删除字符 'c' 。
示例 3：

输入：s = "abc"
输出：false
 

提示：

1 <= s.length <= 105
s 由小写英文字母组成
```

```

```

```
func validPalindrome(s string) bool {
    left := 0
    right := len(s) - 1
    for left < right {
        if s[left] == s[right] {
            left++
            right--
        } else {
            return valid(s, left + 1, right) || valid(s, left, right - 1)
        }
    }
    return true
}

func valid(s string, start int, end int) bool {
    for start < end {
        if s[start] != s[end] {
            return false
        }
        start++
        end--
    }
    return true
}
```
```
给你一个字符串 s，找到 s 中最长的回文子串。

 

示例 1：

输入：s = "babad"
输出："bab"
解释："aba" 同样是符合题意的答案。
示例 2：

输入：s = "cbbd"
输出："bb"
 

提示：

1 <= s.length <= 1000
s 仅由数字和英文字母组成
```

```

```

```
func longestPalindrome(s string) string {
    max_start, max_end := 0,0
    for i := 0; i < len(s); i++ {
        res1_start, res1_end := isPalindrome(s, i, i)
        res2_start, res2_end := isPalindrome(s, i , i + 1)
        if res1_end - res1_start > max_end - max_start {
            max_start = res1_start
            max_end = res1_end
        }
        if res2_end - res2_start > max_end - max_start {
            max_start = res2_start
            max_end = res2_end
        }
    }
    return s[max_start : max_end + 1]
}

func isPalindrome(s string, left int, right int) (int, int){
    for left >= 0 && right < len(s) && s[left] == s[right] {
        left--
        right++
    }
    start := left + 1
    end := right - 1
    return start, end
}
```
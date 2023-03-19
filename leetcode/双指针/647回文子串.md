```
给你一个字符串 s ，请你统计并返回这个字符串中 回文子串 的数目。

回文字符串 是正着读和倒过来读一样的字符串。

子字符串 是字符串中的由连续字符组成的一个序列。

具有不同开始位置或结束位置的子串，即使是由相同的字符组成，也会被视作不同的子串。

 

示例 1：

输入：s = "abc"
输出：3
解释：三个回文子串: "a", "b", "c"
示例 2：

输入：s = "aaa"
输出：6
解释：6个回文子串: "a", "a", "a", "aa", "aa", "aaa"
 

提示：

1 <= s.length <= 1000
s 由小写英文字母组成
```

```

```

```
func countSubstrings(s string) int {
    ret := 0
    for i := 0; i < len(s); i++ {
        left := i
        right := i
        for left >= 0 && right < len(s) && s[left] == s[right] {
            left--
            right++
            ret++
        }
    }
    for i := 0; i < len(s); i++ {
        left := i
        right := i + 1
        for left >= 0 && right < len(s) && s[left] == s[right] {
            left--
            right++
            ret++
        }
    }
    return ret
}
```
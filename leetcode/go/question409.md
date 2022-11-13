```
给定一个包含大写字母和小写字母的字符串 s ，返回 通过这些字母构造成的 最长的回文串 。

在构造过程中，请注意 区分大小写 。比如 "Aa" 不能当做一个回文字符串。

 

示例 1:

输入:s = "abccccdd"
输出:7
解释:
我们可以构造的最长的回文串是"dccaccd", 它的长度是 7。
示例 2:

输入:s = "a"
输入:1
 

提示:

1 <= s.length <= 2000
s 只由小写 和/或 大写英文字母组成
```

```

```

```
func longestPalindrome(s string) int {
    res := 0
	hashmap := make(map[string]int)
	for i := 0; i < len(s); i++ {
		char := string(s[i])
		hashmap[char]++
		if hashmap[char] == 2 {
			res += 2
			hashmap[char] = 0
		}
	}
	if res < len(s) {
		return res + 1
	} else {
		return res
	}
}
```
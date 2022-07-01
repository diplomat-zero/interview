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
class Solution:
    def countSubstrings(self, s: str) -> int:
        s = list(s)
        res = 0
        for i in range(len(s) * 2 - 1):
            left = i // 2
            right = left + i % 2
            while left >= 0 and right < len(s) and s[left] == s[right]:
                res += 1
                left -= 1
                right += 1
        
        return res
```

```
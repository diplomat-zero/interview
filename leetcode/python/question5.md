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
class Solution:
    def longestPalindrome(self, s: str) -> str:
        res = ''
        for i in range(len(s)):
            res1 = self.Palindrome(s, i, i)
            res2 = self.Palindrome(s, i, i + 1)
            if len(res1) > len(res):
                res = res1
            if len(res2) > len(res):
                res = res2
        return res

    
    def Palindrome(self, s, left, right):
        while left >= 0 and right < len(s) and s[left] == s[right]:
            left -= 1
            right += 1
        
        return s[left + 1:right]
```
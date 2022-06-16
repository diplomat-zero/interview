```
给你一个只包含 '(' 和 ')' 的字符串，找出最长有效（格式正确且连续）括号子串的长度。

示例 1：
输入：s = "(()"
输出：2
解释：最长有效括号子串是 "()"

示例 2：
输入：s = ")()())"
输出：4
解释：最长有效括号子串是 "()()"

示例 3：
输入：s = ""
输出：0
 
提示：
0 <= s.length <= 3 * 104
s[i] 为 '(' 或 ')'
```

```

```

```
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        stack = []
        dp = [0 for _ in range(len(s) + 1)]
        for i in range(len(s)):
            if s[i] == '(':
                stack.append(i)
                dp[i + 1] = 0
            else:
                if len(stack) == 0:
                    dp[i + 1] = 0
                else:
                    left = stack.pop()
                    dp[i + 1] = dp[left] + i - left + 1
        
        max_len = 0
        for i in range(len(dp)):
            max_len = max(max_len, dp[i])
        
        return max_len
```
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
class Solution {
    public int longestValidParentheses(String s) {
        int[] dp = new int[s.length() + 1];
        Stack<Integer> stack = new Stack<>();
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                dp[i + 1] = 0;
                stack.push(i);
            } else {
                if (stack.isEmpty()) {
                    dp[i + 1] = 0;
                } else {
                    int left = stack.pop();
                    dp[i + 1] = dp[left] + i - left + 1;
                }
            }
        }
        int res = 0;
        for (int j = 0; j < dp.length; j++) {
            res = Math.max(res, dp[j]);
        }

        return res;
    }
}
```
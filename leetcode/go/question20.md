```
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串 s ，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
 

示例 1：

输入：s = "()"
输出：true
示例 2：

输入：s = "()[]{}"
输出：true
示例 3：

输入：s = "(]"
输出：false
示例 4：

输入：s = "([)]"
输出：false
示例 5：

输入：s = "{[]}"
输出：true
 

提示：

1 <= s.length <= 104
s 仅由括号 '()[]{}' 组成
```

```

```

```
func isValid(s string) bool {
    stack := make([]string, 0)
    for i := 0; i < len(s); i++ {
        char := string(s[i])
        if char == "(" || char == "[" || char == "{" {
            stack = append(stack, char)
        } else {
            if len(stack) == 0 {
                return false
            }
            end := stack[len(stack) - 1]
            if (end == "(" && char == ")") || (end == "[" && char == "]") || (end == "{" && char == "}") {
                stack = stack[:len(stack) - 1]
                continue
            } else {
                return false
            }
        }
    }

    if len(stack) == 0 {
        return true
    }
    return false
}
```
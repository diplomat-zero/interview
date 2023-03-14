```
给你一个由若干括号和字母组成的字符串 s ，删除最小数量的无效括号，使得输入的字符串有效。

返回所有可能的结果。答案可以按 任意顺序 返回。

 

示例 1：

输入：s = "()())()"
输出：["(())()","()()()"]
示例 2：

输入：s = "(a)())()"
输出：["(a())()","(a)()()"]
示例 3：

输入：s = ")("
输出：[""]
 

提示：

1 <= s.length <= 25
s 由小写英文字母以及括号 '(' 和 ')' 组成
s 中至多含 20 个括号
```

```

```

```
func removeInvalidParentheses(s string) []string {
    left_remove := 0
    right_remove := 0
    for _,value := range s {
        if value == '(' {
            left_remove++
        } else if value == ')' && left_remove == 0 {
            right_remove++
        } else if value == ')' && left_remove > 0 {
            left_remove--
        }
    }
    res = make([]string, 0)
    dfs(s, left_remove, right_remove, 0)
    if len(res) == 0 {
        res = append(res, "")
    }
    return res

}
var res []string
func dfs(s string, left_remove int, right_remove int, start int) {
    if left_remove == 0 && right_remove == 0 {
        if isValid(s) {
            res = append(res, s)
            return
        }
    }
    for i := start; i < len(s); i++ {
        if i > start && s[i] == s[i - 1] {
            continue
        }
        if s[i] == '(' && left_remove > 0 {
            dfs(s[:i]+s[i + 1:], left_remove - 1, right_remove, i)
        }
        if s[i] == ')' && right_remove > 0 {
            dfs(s[:i]+s[i + 1:], left_remove, right_remove - 1, i)
        }
    }
}

func isValid(s string) bool {
    left := 0
    for _,value := range s {
        if value == '(' {
            left++
        } else if value == ')' {
            left--
            if left < 0 {
                return false
            }
        }
    }
    return left == 0
}
```
```
数字 n 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 有效的 括号组合。

 

示例 1：

输入：n = 3
输出：["((()))","(()())","(())()","()(())","()()()"]
示例 2：

输入：n = 1
输出：["()"]
 

提示：

1 <= n <= 8
```

```

```

```
func generateParenthesis(n int) []string {
    res = make([]string, 0)
    trace := ""
    dfs(n, n, trace)
    return res
}

var res []string

func dfs(left int, right int, trace string) {
    if left < 0 || right < 0 {
        return
    }

    if left > right {
        return
    } 

    if left == 0 && right == 0 {
        res = append(res, trace)
        return
    }

    trace = trace + "("
    dfs(left - 1, right, trace)
    trace = trace[:len(trace) - 1]

    trace = trace + ")"
    dfs(left, right - 1, trace)
    trace = trace[:len(trace) - 1]
}
```
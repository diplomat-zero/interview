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
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        String trace = "";
        dfs(n, n, trace, result);
        return result;
    }

    public void dfs(int left, int right, String trace, List<String> result) {
        if (left < 0 || right < 0) {
            return;
        }

        if (left > right) {
            return;
        }

        if (left == 0 && right == 0) {
            result.add(trace);
            return;
        }

        trace += '(';
        dfs(left - 1, right, trace, result);
        trace = trace.substring(0, trace.length() - 1);

        trace += ')';
        dfs(left, right - 1, trace, result);
        trace = trace.substring(0, trace.length() - 1);
    }
}
```
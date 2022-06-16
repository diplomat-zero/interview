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
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        self.res = []
        def dfs(left, right, trace):
            if left > right:
                return
            if left < 0 or right < 0:
                return

            if left == 0 and right == 0:
                self.res.append(trace)
            
            trace = trace + '('
            dfs(left - 1, right, trace)
            trace = trace[:-1]

            trace = trace + ')'
            dfs(left, right - 1, trace)
            trace = trace[:-1]
        
        dfs(n, n, '')
        return self.res
```
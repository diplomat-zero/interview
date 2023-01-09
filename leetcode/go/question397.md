```
给定一个正整数 n ，你可以做如下操作：

如果 n 是偶数，则用 n / 2替换 n 。
如果 n 是奇数，则可以用 n + 1或n - 1替换 n 。
返回 n 变为 1 所需的 最小替换次数 。

 

示例 1：

输入：n = 8
输出：3
解释：8 -> 4 -> 2 -> 1
示例 2：

输入：n = 7
输出：4
解释：7 -> 8 -> 4 -> 2 -> 1
或 7 -> 6 -> 3 -> 2 -> 1
示例 3：

输入：n = 4
输出：2
 

提示：

1 <= n <= 231 - 1
```

```

```

```
func integerReplacement(n int) int {
    step := 0
    stack := make([]int, 0)
    stack = append(stack, n)
    visited := make(map[int]bool)
    for len(stack) > 0 {
        length := len(stack)
        for i := 0; i < length; i++ {
            cur := stack[0]
            stack = stack[1:]
            if cur == 1 {
                return step
            }
            if cur % 2 == 0 {
                tmp := cur / 2
                if !visited[tmp] {
                    stack = append(stack, tmp)
                    visited[tmp] = true
                }
            } else {
                tmp := cur - 1
                if !visited[tmp] {
                    stack = append(stack, tmp)
                    visited[tmp] = true
                }
                tmp1 := cur + 1 
                if !visited[tmp1] {
                    stack = append(stack, tmp1)
                    visited[tmp1] = true
                }
            }
        }
        step++
    }
    return -1
}
```
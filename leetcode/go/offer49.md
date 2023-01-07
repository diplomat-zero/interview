```
我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。

 

示例:

输入: n = 10
输出: 12
解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。
说明:  

1 是丑数。
n 不超过1690。
```

```

```

```
func nthUglyNumber(n int) int {
    dp := make([]int, n + 1)
    dp[1] = 1
    p2, p3, p5 := 1, 1, 1
    for i := 2; i <= n; i++ {
        p2_res := dp[p2] * 2
        p3_res := dp[p3] * 3
        p5_res := dp[p5] * 5
        dp[i] = min(p2_res, min(p3_res, p5_res))
        if dp[i] == p2_res {
            p2++
        }
        if dp[i] == p3_res {
            p3++
        }
        if dp[i] == p5_res {
            p5++
        }
    }
    return dp[n]
}

func min(a,b int) int {
    if a < b {
        return a
    }
    return b
}
```
```
给你一个整数 n ，求恰由 n 个节点组成且节点值从 1 到 n 互不相同的 二叉搜索树 有多少种？返回满足题意的二叉搜索树的种数。

 

示例 1：


输入：n = 3
输出：5
示例 2：

输入：n = 1
输出：1
 

提示：

1 <= n <= 19
```

```

```

```
func numTrees(n int) int {
    hash_map := make(map[int]int)
    var count func(int)int
    count = func(n int) int {
        if n <= 1 {
            return 1
        }
        if value,ok := hash_map[n]; ok {
            return value
        }

        res := 0
        for i := 1; i <= n; i++ {
            left_count := count(i - 1)
            right_count := count(n - i)
            res += left_count * right_count
        }
        hash_map[n] = res
        return res
    }
    return count(n)
}
```
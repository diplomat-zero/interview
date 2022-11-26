```
给你一个 32 位的有符号整数 x ，返回将 x 中的数字部分反转后的结果。

如果反转后整数超过 32 位的有符号整数的范围 [−231,  231 − 1] ，就返回 0。

假设环境不允许存储 64 位整数（有符号或无符号）。
 

示例 1：

输入：x = 123
输出：321
示例 2：

输入：x = -123
输出：-321
示例 3：

输入：x = 120
输出：21
示例 4：

输入：x = 0
输出：0
 

提示：

-231 <= x <= 231 - 1
```

```

```

```
func reverse(x int) int {
    fu := false
    if x < 0 {
        fu = true
        x = -x
    }
    x_s := strconv.Itoa(x)

    left := 0
    right := len(x_s) - 1
    r := []rune(x_s)
    for left < right {
        r[left], r[right] = r[right], r[left]
        left++
        right--
    }
    x_s_s := string(r)
    res,_ := strconv.Atoi(x_s_s)
    if fu {
        res = -res
    }

    if res > math.MaxInt32 {
        return 0
    }
    if res < math.MinInt32 {
        return 0
    }
    return res

}
```
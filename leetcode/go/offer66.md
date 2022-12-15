```
给定一个数组 A[0,1,…,n-1]，请构建一个数组 B[0,1,…,n-1]，其中 B[i] 的值是数组 A 中除了下标 i 以外的元素的积, 即 B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]。不能使用除法。

 

示例:

输入: [1,2,3,4,5]
输出: [120,60,40,30,24]
 

提示：

所有元素乘积之和不会溢出 32 位整数
a.length <= 100000
```

```

```

```
func constructArr(a []int) []int {
    if len(a) == 0 {
        return []int{}
    }
    left := make([]int, len(a))
    right := make([]int, len(a))
    left[0] = 1
    right[len(a) - 1] = 1
    for i := 1; i < len(a); i++ {
        left[i] = left[i - 1] * a[i - 1]
    }
    for i := len(a) - 2; i >= 0; i-- {
        right[i] = right[i + 1] * a[i + 1]
    }
    res := make([]int, len(a))
    for i := 0; i < len(a); i++ {
        res[i] = left[i] * right[i]
    }
    return res
}
```
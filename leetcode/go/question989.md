```
整数的 数组形式  num 是按照从左到右的顺序表示其数字的数组。

例如，对于 num = 1321 ，数组形式是 [1,3,2,1] 。
给定 num ，整数的 数组形式 ，和整数 k ，返回 整数 num + k 的 数组形式 。

 

示例 1：

输入：num = [1,2,0,0], k = 34
输出：[1,2,3,4]
解释：1200 + 34 = 1234
示例 2：

输入：num = [2,7,4], k = 181
输出：[4,5,5]
解释：274 + 181 = 455
示例 3：

输入：num = [2,1,5], k = 806
输出：[1,0,2,1]
解释：215 + 806 = 1021
 

提示：

1 <= num.length <= 104
0 <= num[i] <= 9
num 不包含任何前导零，除了零本身
1 <= k <= 104
```

```

```

```
func addToArrayForm(num []int, k int) []int {
    s := strconv.Itoa(k)
    num1 := make([]int, 0)
    for i := 0; i < len(s); i++ {
        n,_ := strconv.Atoi(string(s[i]))
        num1 = append(num1, n)
    }
    res := make([]int, 0)
    i := len(num) - 1
    j := len(num1) - 1
    jin := 0
    for i >= 0 || j >= 0 || jin != 0 {
        num_i := 0
        if i >= 0 {
            num_i = num[i]
        }
        num_j := 0
        if j >= 0 {
            num_j = num1[j]
        }
        tmp := num_i + num_j + jin
        value := 0
        if tmp >= 10 {
            value = tmp - 10
            jin = 1
        } else {
            value = tmp
            jin = 0
        }
        res = append(res, value)
        i--
        j--
    }
    left := 0
    right := len(res) - 1
    for left < right {
        res[left], res[right] = res[right], res[left]
        left++
        right--
    }
    return res
}
```
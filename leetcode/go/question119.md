```
给定一个非负索引 rowIndex，返回「杨辉三角」的第 rowIndex 行。

在「杨辉三角」中，每个数是它左上方和右上方的数的和。



 

示例 1:

输入: rowIndex = 3
输出: [1,3,3,1]
示例 2:

输入: rowIndex = 0
输出: [1]
示例 3:

输入: rowIndex = 1
输出: [1,1]
 

提示:

0 <= rowIndex <= 33
 

进阶：

你可以优化你的算法到 O(rowIndex) 空间复杂度吗？
```

```

```

```
func getRow(rowIndex int) []int {
    if rowIndex == 0 {
        return []int{1}
    }
    res := make([][]int, rowIndex + 1)
    for i := 0; i < len(res); i++ {
        res[i] = make([]int, i + 1)
    }
    for i := 0; i <= rowIndex; i++ {
        res[i][0] = 1
        res[i][i] = 1
    }
    for i := 2; i <= rowIndex; i++ {
        for j := 1; j < i; j++ {
            res[i][j] = res[i - 1][j] + res[i - 1][j - 1]
        }
    }
    return res[rowIndex]
}
```
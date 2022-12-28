```
给定一个非负整数 numRows，生成「杨辉三角」的前 numRows 行。

在「杨辉三角」中，每个数是它左上方和右上方的数的和。



 

示例 1:

输入: numRows = 5
输出: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
示例 2:

输入: numRows = 1
输出: [[1]]
 

提示:

1 <= numRows <= 30
```

```

```

```
func generate(numRows int) [][]int {
    res := make([][]int, numRows)
    for i := 0; i < len(res); i++ {
        res[i] = make([]int, i + 1)
    }
    for i := 0; i < numRows; i++ {
        res[i][0] = 1
        res[i][i] = 1
    }
    for i := 2; i < numRows; i++ {
        for j := 1; j < i; j++ {
            res[i][j] = res[i - 1][j] + res[i - 1][j - 1]
        }
    }
    return res
}
```
```
在一个由 '0' 和 '1' 组成的二维矩阵内，找到只包含 '1' 的最大正方形，并返回其面积。

 

示例 1：


输入：matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
输出：4
示例 2：


输入：matrix = [["0","1"],["1","0"]]
输出：1
示例 3：

输入：matrix = [["0"]]
输出：0
 

提示：

m == matrix.length
n == matrix[i].length
1 <= m, n <= 300
matrix[i][j] 为 '0' 或 '1'
```

```

```

```
class Solution:
    def maximalSquare(self, matrix: List[List[str]]) -> int:
        dp = [[0] * len(matrix[0]) for _ in range(len(matrix))]

        for i in range(len(matrix)):
            dp[i][0] = int(matrix[i][0])
        
        for j in range(len(matrix[0])):
            dp[0][j] = int(matrix[0][j])
        
        
        for m in range(1, len(matrix)):
            for n in range(1, len(matrix[0])):
                if matrix[m][n] == '0':
                    dp[m][n] = 0
                else:
                    dp[m][n] = min(dp[m - 1][n], dp[m][n - 1], dp[m - 1][n - 1]) + 1
                    
        length = 0
        for p in range(len(dp)):
            for q in range(len(dp[0])):
                length = max(length, dp[p][q])

        return length * length
```
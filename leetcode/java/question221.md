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
class Solution {
    public int maximalSquare(char[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;
        int[][]dp = new int[m][n];
        for (int i = 0; i < m; i++) {
            dp[i][0] = matrix[i][0] - '0';
        }
        for (int j = 0; j < n; j++) {
            dp[0][j] = matrix[0][j] - '0';
        }

        for (int p = 1; p < m; p++) {
            for (int q = 1; q < n; q++) {
                if (matrix[p][q] == '0') {
                    continue;
                }
                dp[p][q] = Math.min(dp[p - 1][q - 1], Math.min(dp[p][q - 1], dp[p - 1][q])) + 1;
            }
        }

        int res = 0;
        for (int i = 0; i < dp.length; i++) {
            for (int j = 0; j < dp[0].length; j++) {
                res = Math.max(res, dp[i][j]);
            }
        }
        return res * res;
    }
}
```
```
一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为 “Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

网格中的障碍物和空位置分别用 1 和 0 来表示。

 

示例 1：


输入：obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]
输出：2
解释：3x3 网格的正中间有一个障碍物。
从左上角到右下角一共有 2 条不同的路径：
1. 向右 -> 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右 -> 向右
示例 2：


输入：obstacleGrid = [[0,1],[0,0]]
输出：1
 

提示：

m == obstacleGrid.length
n == obstacleGrid[i].length
1 <= m, n <= 100
obstacleGrid[i][j] 为 0 或 1
```

```

```

```
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        m = len(obstacleGrid)
        n = len(obstacleGrid[0])
        dp = [[0] * n for _ in range(m)]
        x = False
        for i in range(0, m):
            if x:
                dp[i][0] = 0
                continue
            
            if obstacleGrid[i][0] == 1:
                dp[i][0] = 0
                x = True
            else:
                dp[i][0] = 1
        
        y = False
        for j in range(0, n):
            if y:
                dp[0][j] = 0
                continue
            
            if obstacleGrid[0][j] == 1:
                dp[0][j] = 0
                y = True
            else:
                dp[0][j] = 1
        
        for p in range(1, m):
            for q in range(1, n):
                if obstacleGrid[p][q] == 1:
                    dp[p][q] = 0
                else:
                    dp[p][q] = dp[p - 1][q] + dp[p][q - 1]
        
        return dp[m - 1][n - 1]
```
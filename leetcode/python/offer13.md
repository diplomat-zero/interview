```
地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

示例 1：
输入：m = 2, n = 3, k = 1
输出：3

示例 2：
输入：m = 3, n = 1, k = 0
输出：1

提示：
1 <= n,m <= 100
0 <= k <= 20
```

```
class Solution:

    def movingCount(self, m: int, n: int, k: int) -> int:
        visited = [[False for _ in range(n)] for _ in range(m)]
        return self.dfs(0, 0, m, n, k, visited)
        


    def dfs(self, x: int, y: int, m: int, n: int, k: int, visited) -> int:
        ret = self.caculate(x, y)
        if x < 0 or y < 0 or x >= m or y >= n or ret > k or visited[x][y] == True:
            return 0

        visited[x][y] = True
        return self.dfs(x + 1, y, m, n, k, visited) + self.dfs(x - 1, y, m, n, k, visited) + self.dfs(x, y + 1, m, n, k, visited) + self.dfs(x, y - 1, m, n, k, visited) + 1

    def caculate(self, x: int, y: int) -> int:
        if x == 100:
            numx = 1
        else:
            numx = x // 10 + x % 10
        if y == 100:
            numy = 1
        else:
            numy = y // 10 + y % 10
            
        return numx + numy
```
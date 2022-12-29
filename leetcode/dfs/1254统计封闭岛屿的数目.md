```
二维矩阵 grid 由 0 （土地）和 1 （水）组成。岛是由最大的4个方向连通的 0 组成的群，封闭岛是一个 完全 由1包围（左、上、右、下）的岛。

请返回 封闭岛屿 的数目。

 

示例 1：



输入：grid = [[1,1,1,1,1,1,1,0],[1,0,0,0,0,1,1,0],[1,0,1,0,1,1,1,0],[1,0,0,0,0,1,0,1],[1,1,1,1,1,1,1,0]]
输出：2
解释：
灰色区域的岛屿是封闭岛屿，因为这座岛屿完全被水域包围（即被 1 区域包围）。
示例 2：



输入：grid = [[0,0,1,0,0],[0,1,0,1,0],[0,1,1,1,0]]
输出：1
示例 3：

输入：grid = [[1,1,1,1,1,1,1],
             [1,0,0,0,0,0,1],
             [1,0,1,1,1,0,1],
             [1,0,1,0,1,0,1],
             [1,0,1,1,1,0,1],
             [1,0,0,0,0,0,1],
             [1,1,1,1,1,1,1]]
输出：2
 

提示：

1 <= grid.length, grid[0].length <= 100
0 <= grid[i][j] <=1
```

```

```

```
func closedIsland(grid [][]int) int {
    for i := 0; i < len(grid); i++ {
        if grid[i][0] == 0 {
            dfs(grid, i, 0)
        }
        if grid[i][len(grid[0]) - 1] == 0 {
            dfs(grid, i, len(grid[0]) - 1)
        }
    }
    for j := 0; j < len(grid[0]); j++ {
        if grid[0][j] == 0 {
            dfs(grid, 0, j)
        }
        if grid[len(grid) - 1][j] == 0 {
            dfs(grid, len(grid) - 1, j)
        }
    }
    res := 0
    for i := 1; i < len(grid) - 1; i++ {
        for j := 1; j < len(grid[0]) - 1; j++ {
            if grid[i][j] == 0 {
                dfs(grid, i, j)
                res++
            }   
        }
    }
    return res
}

func dfs(grid [][]int, i int, j int) {
    if i < 0 || j < 0 || i >= len(grid) || j >= len(grid[0]) || grid[i][j] == 1 {
        return 
    }
    
    grid[i][j] = 1
    dfs(grid, i + 1, j)
    dfs(grid, i - 1, j)
    dfs(grid, i, j + 1)
    dfs(grid, i, j - 1)
}
```
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
var visited [][]bool
var num int
func movingCount(m int, n int, k int) int {
	x := 0
	y := 0
	num = 0

	visited = make([][]bool, m)
	for i := 0; i < len(visited); i++ {
		visited[i] = make([]bool, n)
	}

	dfs(x, y, m, n, k)
    return num
}

func dfs(x int, y int, m int, n int, k int) bool {
	res := caculate(x, y)
	if x < 0 || y < 0 || x >= m || y >= n || res > k {
		return false
	}

	if visited[x][y] {
		return false
	}

	visited[x][y] = true
	num++
	
	dfs(x + 1, y, m, n, k)
	dfs(x - 1, y, m, n, k)
	dfs(x, y + 1, m, n, k)
	dfs(x, y - 1, m, n, k)
	return true
}

func caculate(x int, y int) int {
	stringx := strconv.Itoa(x)
	stringy := strconv.Itoa(y)

	sum := 0
	for _, ch1 := range stringx {
		ch1int, _ := strconv.Atoi(string(ch1))
		sum += ch1int
	}

	for _, ch2 := range stringy {
		ch2int, _ := strconv.Atoi(string(ch2))
		sum += ch2int
	}

	return sum
}
```
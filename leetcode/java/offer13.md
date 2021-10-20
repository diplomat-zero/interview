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
class Solution {
    boolean[][] visited;
    int num;
    public int movingCount(int m, int n, int k) {
        int x = 0;
        int y = 0;

        this.visited = new boolean[m][n];
        dfs(x, y, m, n, k);
        return this.num;
    }

    public void dfs(int x, int y, int m, int n, int k) {
        int res = caculate(x, y);
        if (x < 0 || y < 0 || x >=m || y >= n || res > k) {
            return;
        }

        if (this.visited[x][y]) {
            return;
        }
        this.visited[x][y] = true;
        this.num++;
        dfs(x + 1, y, m, n, k);
        dfs(x - 1, y, m, n, k);
        dfs(x, y + 1, m, n, k);
        dfs(x, y - 1, m, n, k);
    }

    public static int caculate(int x, int y) {
        String stringx = Integer.toString(x);
        String stringy = Integer.toString(y);

        int sum = 0;
        for (int i = 0; i < stringx.length(); i++) {
            int numx = stringx.charAt(i) - '0';
            sum += numx;
        }
        for (int j = 0; j < stringy.length(); j++) {
            int numy = stringy.charAt(j) - '0';
            sum += numy;
        }

        return sum;
    } 
}
```
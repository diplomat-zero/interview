```
给定一个 m x n 二维字符网格 board 和一个字符串单词 word 。如果 word 存在于网格中，返回 true ；否则，返回 false 。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

 

示例 1：


输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：true
示例 2：


输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
输出：true
示例 3：


输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
输出：false
 

提示：

m == board.length
n = board[i].length
1 <= m, n <= 6
1 <= word.length <= 15
board 和 word 仅由大小写英文字母组成
 

进阶：你可以使用搜索剪枝的技术来优化解决方案，使其在 board 更大的情况下可以更快解决问题？
```

```

```

```
class Solution {
    boolean res = false;
    public boolean exist(char[][] board, String word) {
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                if (board[i][j] == word.charAt(0)) {
                    dfs(board, i, j, word, 0);
                }
            }
        }
        return res;
    }

    public void dfs(char[][] board, int i, int j, String word, int m) {
        if (i < 0 || j < 0 || i >= board.length || j >= board[0].length || m >= word.length()) {
            return;
        }
        if (board[i][j] != word.charAt(m)) {
            return;
        }
        if (word.length() - 1 == m) {
            res = true;
            return;
        }

        char tmp = board[i][j];

        board[i][j] = '#';
        dfs(board, i + 1, j, word, m + 1);
        board[i][j] = tmp;

        board[i][j] = '#';
        dfs(board, i - 1, j, word, m + 1);
        board[i][j] = tmp;

        board[i][j] = '#';
        dfs(board, i, j + 1, word, m + 1);
        board[i][j] = tmp;

        board[i][j] = '#';
        dfs(board, i, j - 1, word, m + 1);
        board[i][j] = tmp;
    }
}
```
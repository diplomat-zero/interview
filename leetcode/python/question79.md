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
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        self.res = False
        def dfs(board, i, j, word, m):
            if i < 0 or j < 0 or i >= len(board) or j >= len(board[0]) or board[i][j] != word[m]:
                return
            
            if m == len(word) - 1:
                self.res = True
                return
            
            tmp = board[i][j]
            board[i][j] = '0'
            dfs(board, i + 1, j, word, m + 1)
            board[i][j] = tmp
            board[i][j] = '0'
            dfs(board, i - 1, j, word, m + 1)
            board[i][j] = tmp
            board[i][j] = '0'
            dfs(board, i, j + 1, word, m + 1)
            board[i][j] = tmp
            board[i][j] = '0'
            dfs(board, i, j - 1, word, m + 1)
            board[i][j] = tmp
        
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] == word[0]:
                    dfs(board, i, j, word, 0)
    
        return self.res
```
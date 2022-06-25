```
给你一个正整数 n ，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的 n x n 正方形矩阵 matrix 。

 

示例 1：


输入：n = 3
输出：[[1,2,3],[8,9,4],[7,6,5]]
示例 2：

输入：n = 1
输出：[[1]]
 

提示：

1 <= n <= 20
```

```

```

```
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        matrix = [[0] * n for _ in range(n)]

        total = n * n
        left = 0
        right = n - 1
        top = 0
        bottom = n - 1
        num = 1
        while total >= 1:
            i = left
            while i <= right and total >= 1:
                matrix[top][i] = num
                num += 1
                total -= 1
                i += 1
            top += 1
            
            i = top
            while i <= bottom and total >= 1:
                matrix[i][right] = num
                num += 1
                total -= 1
                i += 1
            right -= 1

            i = right
            while i >= left and total >= 1:
                matrix[bottom][i] = num
                num += 1
                total -= 1
                i -= 1
            bottom -= 1
            
            i = bottom
            while i >= top and total >= 1:
                matrix[i][left] = num
                num += 1
                total -= 1
                i -= 1
            left += 1
        return matrix
```
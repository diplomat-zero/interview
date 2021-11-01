```
输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

示例 1：
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]

示例 2：
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
 
限制：
0 <= matrix.length <= 100
0 <= matrix[i].length <= 100
```

```
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        ret = []
        if len(matrix) == 0 or len(matrix[0]) == 0:
            return ret

        top = 0
        bottom = len(matrix) - 1

        left = 0
        right = len(matrix[0]) - 1

        total = len(matrix) * len(matrix[0])

        

        while total > 0:
            i = left
            while i <= right and i >= left and total > 0:
                ret.append(matrix[top][i])
                total -= 1
                i += 1
            top += 1

            i = top            
            while i <= bottom and i >= top and total > 0:
                ret.append(matrix[i][right])
                total -= 1
                i += 1
            right -= 1
            
            i = right
            while i <= right and i >= left and total > 0:
                ret.append(matrix[bottom][i])
                total -= 1
                i -= 1
            bottom -= 1
              
            i = bottom
            while i <= bottom and i >= top and total > 0:
                ret.append(matrix[i][left])
                total -= 1
                i -= 1
            left += 1

        
        return ret
```
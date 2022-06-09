```
给你一个 m 行 n 列的矩阵 matrix ，请按照 顺时针螺旋顺序 ，返回矩阵中的所有元素。

示例 1：
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]

示例 2：
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
 
提示：
m == matrix.length
n == matrix[i].length
1 <= m, n <= 10
-100 <= matrix[i][j] <= 100
```

```
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        left = 0
        right = len(matrix[0]) - 1
        top = 0
        bottom = len(matrix) - 1
        total = len(matrix) * len(matrix[0])
        ret = []
        while total >= 1 :
            for i in range(left, right + 1):
                if total >= 1:
                    ret.append(matrix[top][i])
                    total -= 1
            top += 1
            for i in range(top, bottom + 1):
                if total >= 1:
                    ret.append(matrix[i][right])
                    total -= 1
            right -= 1
            i = right
            while i >= left and i <= right and total >= 1:
                ret.append(matrix[bottom][i])
                total -= 1
                i -= 1
            bottom -= 1
            i = bottom
            while i >= top and i <= bottom and total >= 1:
                ret.append(matrix[i][left])
                total -= 1
                i -= 1
            left += 1
        
        return ret
```

```
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        left = 0
        right = len(matrix[0]) - 1
        top = 0
        bottom = len(matrix) - 1
        total = len(matrix) * len(matrix[0])
        res = []
        while total >= 1:
            i = left
            while i >= left and i <= right and total >= 1:
                res.append(matrix[top][i])
                total -= 1
                i += 1
            top += 1

            i = top
            while i >= top and i <= bottom and total >= 1:
                res.append(matrix[i][right])
                total -= 1
                i += 1
            right -= 1

            i = right
            while i >= left and i <= right and total >= 1:
                res.append(matrix[bottom][i])
                total -= 1
                i -= 1
            bottom -= 1

            i = bottom
            while i >= top and i <= bottom and total >= 1:
                res.append(matrix[i][left])
                total -= 1
                i -= 1
            left += 1
        
        return res
```
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
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        int left = 0;
        int right = matrix[0].length - 1;
        int top = 0;
        int bottom = matrix.length - 1;
        int total = matrix.length * matrix[0].length;
        List<Integer> ret = new ArrayList<>();
        while (total >= 1) {
            for (int i = left; i <= right && total >= 1; i++) {
                ret.add(matrix[top][i]);
                total--;
            }
            top++;
            for (int i = top; i <= bottom && total >= 1; i++) {
                ret.add(matrix[i][right]);
                total--;
            }
            right--;
            for (int i = right; i >= left && total >= 1; i--) {
                ret.add(matrix[bottom][i]);
                total--;
            }
            bottom--;
            for (int i = bottom; i >= top && total >= 1; i--) {
                ret.add(matrix[i][left]);
                total--;
            }
            left++;
        }

        return ret;
    }
}
```
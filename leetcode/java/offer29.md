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
class Solution {
    public int[] spiralOrder(int[][] matrix) {
        if (matrix.length == 0 || matrix[0].length == 0) {
            int[] ret = new int[0];
            return ret;
        }

        int top = 0;
        int buttom = matrix.length - 1;

        int left = 0;
        int right = matrix[0].length - 1;

        int total = matrix.length * matrix[0].length;

        ArrayList<Integer> ret = new ArrayList<>();

        while (total >= 1) {
            for (int i = left; i <= right && total >= 1; i++) {
                ret.add(matrix[top][i]);
                total--;
            }
            top++;
            for (int i = top; i <= buttom && total >= 1; i++) {
                ret.add(matrix[i][right]);
                total--;
            }
            right--;
            for (int i = right; i >= left && total >= 1; i--) {
                ret.add(matrix[buttom][i]);
                total--;
            }
            buttom--;
            for (int i = buttom; i >= top && total >= 1; i--) {
                ret.add(matrix[i][left]);
                total--;
            }
            left++;
        }

        int[] res = new int[ret.size()];
        for (int i = 0; i < ret.size(); i++) {
            res[i] = ret.get(i);
        }
        return res;
    }
}
```
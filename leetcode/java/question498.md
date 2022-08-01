```
给你一个大小为 m x n 的矩阵 mat ，请以对角线遍历的顺序，用一个数组返回这个矩阵中的所有元素。

 

示例 1：


输入：mat = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,4,7,5,3,6,8,9]
示例 2：

输入：mat = [[1,2],[3,4]]
输出：[1,2,3,4]
 

提示：

m == mat.length
n == mat[i].length
1 <= m, n <= 104
1 <= m * n <= 104
-105 <= mat[i][j] <= 105
```

```

```

```
class Solution {
    public int[] findDiagonalOrder(int[][] mat) {
        LinkedHashMap<Integer, List<Integer>> result = new LinkedHashMap<>();
        for (int i = 0; i < mat.length; i++) {
            for (int j = 0; j < mat[0].length; j++) {
                List<Integer> tmp;
                if (result.containsKey(i + j)) {
                    tmp = result.get(i + j);
                } else {
                    tmp = new ArrayList<>();
                }
                tmp.add(mat[i][j]);
                result.put(i + j, tmp);
            }
        }
        List<Integer> res = new ArrayList<>();
        for (int m = 0; m < result.size(); m++) {
            List<Integer> tmp = result.get(m);
            if (m % 2 == 0) {
                for (int q = tmp.size() - 1; q >= 0; q--) {
                    res.add(tmp.get(q));
                }
            } else {
                res.addAll(tmp);
            }
        }

        int[] ans = new int[res.size()];
        for (int i = 0; i < res.size(); i++) {
            ans[i] = res.get(i);
        }
        return ans;
    }
}
```
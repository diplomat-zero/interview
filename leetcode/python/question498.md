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
class Solution:
    def findDiagonalOrder(self, mat: List[List[int]]) -> List[int]:
        mat_dict = {}
        for i in range(len(mat)):
            for j in range(len(mat[0])):
                sum_num = i + j
                if sum_num in mat_dict:
                    mat_dict[sum_num].append(mat[i][j])
                else:
                    mat_dict[sum_num] = []
                    mat_dict[sum_num].append(mat[i][j])
        
        res = []
        for key, value in mat_dict.items():
            if key % 2 == 1:
                for i in range(len(value)):
                    res.append(value[i])
            else:
                i = len(value) - 1
                while i >= 0:
                    res.append(value[i])
                    i -= 1
        
        return res
```
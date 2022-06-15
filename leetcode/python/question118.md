```
给定一个非负整数 numRows，生成「杨辉三角」的前 numRows 行。

在「杨辉三角」中，每个数是它左上方和右上方的数的和。

示例 1:
输入: numRows = 5
输出: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]

示例 2:
输入: numRows = 1
输出: [[1]]
 
提示:
1 <= numRows <= 30
```

```

```

```
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        res = [[1]]
        for i in range(2, numRows + 1):
            res.append([0] * i)
        
        for p in range(1, numRows):
            for q in range(p + 1):
                if q == 0:
                    res[p][q] = 1
                elif q == p:
                    res[p][q] = 1
                else:
                    res[p][q] = res[p - 1][q] + res[p - 1][q - 1]
        
        return res
```
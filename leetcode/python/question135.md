```
n 个孩子站成一排。给你一个整数数组 ratings 表示每个孩子的评分。

你需要按照以下要求，给这些孩子分发糖果：

每个孩子至少分配到 1 个糖果。
相邻两个孩子评分更高的孩子会获得更多的糖果。
请你给每个孩子分发糖果，计算并返回需要准备的 最少糖果数目 。

 

示例 1：

输入：ratings = [1,0,2]
输出：5
解释：你可以分别给第一个、第二个、第三个孩子分发 2、1、2 颗糖果。
示例 2：

输入：ratings = [1,2,2]
输出：4
解释：你可以分别给第一个、第二个、第三个孩子分发 1、2、1 颗糖果。
     第三个孩子只得到 1 颗糖果，这满足题面中的两个条件。
 

提示：

n == ratings.length
1 <= n <= 2 * 104
0 <= ratings[i] <= 2 * 104
```

```

```

```
class Solution:
    def candy(self, ratings: List[int]) -> int:
        map_ratings = [1 for _ in range(len(ratings))]
        
        i = 0
        while i < len(ratings) - 1:
            if ratings[i + 1] > ratings[i]:
                map_ratings[i + 1] = map_ratings[i] + 1
            i += 1
        
        j = len(ratings) - 1
        while j > 0:
            if ratings[j - 1] > ratings[j]:
                map_ratings[j - 1] = max(map_ratings[j - 1], map_ratings[j] + 1)
            j -= 1
        
        res = 0
        for m in range(len(map_ratings)):
            res += map_ratings[m]
        
        return res
```
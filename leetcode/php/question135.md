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
class Solution {

    /**
     * @param Integer[] $ratings
     * @return Integer
     */
    function candy($ratings) {
        $map = [];
        for ($i = 0; $i < count($ratings); $i++) {
            $map[$i]['count'] = 1;
        }

        for ($m = 0; $m < count($ratings) - 1; $m++) {
            if ($ratings[$m + 1] > $ratings[$m]) {
                $map[$m + 1]['count'] = $map[$m]['count'] + 1;
            }
        }

        for ($n = count($ratings) - 1; $n > 0; $n--) {
            if ($ratings[$n - 1] > $ratings[$n]) {
                $map[$n - 1]['count'] = max($map[$n - 1]['count'], $map[$n]['count'] + 1);
            }
        }

        $total = 0;
        foreach ($map as $value) {
            $total += $value['count'];
        }

        return $total;
    }
}
```
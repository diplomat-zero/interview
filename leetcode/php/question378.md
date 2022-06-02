```
给你一个 n x n 矩阵 matrix ，其中每行和每列元素均按升序排序，找到矩阵中第 k 小的元素。
请注意，它是 排序后 的第 k 小元素，而不是第 k 个 不同 的元素。

你必须找到一个内存复杂度优于 O(n2) 的解决方案。

示例 1：
输入：matrix = [[1,5,9],[10,11,13],[12,13,15]], k = 8
输出：13
解释：矩阵中的元素为 [1,5,9,10,11,12,13,13,15]，第 8 小元素是 13

示例 2：
输入：matrix = [[-5]], k = 1
输出：-5
 
提示：
n == matrix.length
n == matrix[i].length
1 <= n <= 300
-109 <= matrix[i][j] <= 109
题目数据 保证 matrix 中的所有行和列都按 非递减顺序 排列
1 <= k <= n2
 
进阶：
你能否用一个恒定的内存(即 O(1) 内存复杂度)来解决这个问题?
你能在 O(n) 的时间复杂度下解决这个问题吗?这个方法对于面试来说可能太超前了，但是你会发现阅读这篇文章（ this paper ）很有趣。
```

```
思路非常简单：

找出二维矩阵中最小的数 left，最大的数 right，那么第 k 小的数必定在 left ~ right 之间
mid=(left+right) / 2；在二维矩阵中寻找小于等于 mid 的元素个数 count
若这个 count 小于 k，表明第 k 小的数在右半部分且不包含 mid，即 left=mid+1, right=right，又保证了第 k 小的数在 left ~ right 之间
若这个 count 大于 k，表明第 k 小的数在左半部分且可能包含 mid，即 left=left, right=mid，又保证了第 k 小的数在 left~right 之间
因为每次循环中都保证了第 k 小的数在 left ~ right 之间，当 left==right 时，第 k 小的数即被找出，等于 right
注意：这里的 left mid right 是数值，不是索引位置。
```

```
class Solution {

    /**
     * @param Integer[][] $matrix
     * @param Integer $k
     * @return Integer
     */
    function kthSmallest($matrix, $k) {
        $row = count($matrix);
        $col = count($matrix[0]);
        $left = $matrix[0][0];
        $right = $matrix[$row - 1][$col - 1];
        while ($left < $right) {
            $mid = floor(($right - $left) / 2 + $left);
            $count = $this->findMid($matrix, $mid, $row, $col);
            if ($count < $k) {
                $left = $mid + 1;
            } else {
                $right = $mid;
            }
        }
        return $right;
    }

    function findMid($matrix, $mid, $row, $col) {
        $i = $row - 1;
        $j = 0;
        $count = 0;
        while ($i >= 0 && $j < $col) {
            if ($matrix[$i][$j] <= $mid) {
                $count += $i + 1;
                $j++;
            } else {
                $i--;
            }
        }
        return $count;
    }
}
```
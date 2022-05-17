```
给定整数 n 和 k，返回  [1, n] 中字典序第 k 小的数字。

示例 1:
输入: n = 13, k = 2
输出: 10
解释: 字典序的排列是 [1, 10, 11, 12, 13, 2, 3, 4, 5, 6, 7, 8, 9]，所以第二小的数字是 10。

示例 2:
输入: n = 1, k = 1
输出: 1
 
提示:
1 <= k <= n <= 109
```

```
思路
字典树
```

```
class Solution {

    /**
     * @param Integer $n
     * @param Integer $k
     * @return Integer
     */
    function findKthNumber($n, $k) {
        $p = 1;
        $prefix = 1;
        while ($p < $k) {
            $count = $this->find($prefix, $n);
            if ($p + $count > $k) {
                $prefix *= 10;
                $p++;
            } else {
                $prefix++;
                $p += $count;
            }
        }
        return $prefix;
    }

    function find($prefix, $n) {
        $count = 0;
        for ($cur = $prefix, $next = $prefix + 1; $cur <= $n; $cur *= 10, $next *= 10) {
            $count += min($next, $n + 1) - $cur;
        }
        return $count;
    }
}
```
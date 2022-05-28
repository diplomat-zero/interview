```
给你一个整数 n ，求恰由 n 个节点组成且节点值从 1 到 n 互不相同的 二叉搜索树 有多少种？返回满足题意的二叉搜索树的种数。

示例 1：
输入：n = 3
输出：5

示例 2：
输入：n = 1
输出：1
 
提示：
1 <= n <= 19
```

```

```

```
class Solution {

    /**
     * @param Integer $n
     * @return Integer
     */
    function numTrees($n) {
        $map = [];
        return $this->count(1, $n, $map);
    }

    function count($lo, $hi, &$map) {
        if ($lo > $hi) {
            return 1;
        }

        if (isset($map[$lo][$hi])) {
            return $map[$lo][$hi];
        }
        $res = 0;
        for ($i = $lo; $i <= $hi; $i++) {
            $left = $this->count($lo, $i - 1, $map);
            $right = $this->count($i + 1, $hi, $map);
            $res += $left * $right;
        }
        $map[$lo][$hi] = $res;
        return $res;
    }
}
```
```
写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项（即 F(N)）。斐波那契数列的定义如下：
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。
答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

示例 1：
输入：n = 2
输出：1

示例 2：
输入：n = 5
输出：5
 
提示：
0 <= n <= 100
```

```
class Solution {

    /**
     * @param Integer $n
     * @return Integer
     */
    function fib($n) {
        if ($n <= 1) {
            return $n;
        }

        $p = 0;
        $q = 0;
        $r = 1;
        for ($m = 2; $m <= $n; $m++) {
            $p = $q;
            $q = $r;
            $r = ($p + $q) % 1000000007;
        }

        return $r;
    }
}
```

```
class Solution {

    /**
     * @param Integer $n
     * @return Integer
     */
    public $arr = [];
    function fib($n) {
        if (isset($this->arr[$n])) {
            return $this->arr[$n];
        }
        if ($n <= 1) {
            $this->arr[$n] = $n;
            return $n;
        }

        $this->arr[$n] = $this->fib($n - 1) + $this->fib($n - 2);
        return $this->arr[$n] % 1000000007;
    }
}
```
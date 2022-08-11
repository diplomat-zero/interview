```
实现 pow(x, n) ，即计算 x 的整数 n 次幂函数（即，xn ）。

 

示例 1：

输入：x = 2.00000, n = 10
输出：1024.00000
示例 2：

输入：x = 2.10000, n = 3
输出：9.26100
示例 3：

输入：x = 2.00000, n = -2
输出：0.25000
解释：2-2 = 1/22 = 1/4 = 0.25
 

提示：

-100.0 < x < 100.0
-231 <= n <= 231-1
-104 <= xn <= 104
```

```

```

```
class Solution {
    public double myPow(double x, int n) {
        long N = n;
        return Pow(x, N);
    }

    public double Pow(double x, long N) {
        if (N == 0) {
            return 1;
        }
        if (N == 1) {
            return x;
        }
        if (N < 0) {
            N = -N;
            x = 1 / x;
        }
        if (N % 2 == 0) {
            return Pow(x * x, N / 2);
        } else {
            return x * Pow(x * x, (N - 1) / 2);
        }
    }
}
```
```
给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0]*k[1]*...*k[m-1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

示例 1：
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1

示例 2:
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36

提示：
2 <= n <= 58
```

```
class Solution {
    public int cuttingRope(int n) {
        Map<Integer, Integer> map = new HashMap<>();
        if (n == 2) {
            map.put(n, 1);
            return 1;
        }
        if (n == 3) {
            map.put(n, 2);
            return 2;
        }
        if (n == 4) {
            map.put(n, 4);
            return 4;
        }
        if (map.containsKey(n)) {
            return map.get(n);
        }
        int maxnum = 2 * (n - 2);
        if (n > 5) {
            int tmp = 3 * (n - 3);
            int tmp1 = 0;
            if (n - 3 > 4) {
                tmp1 = 3 * cuttingRope(n - 3);
            }
            maxnum = Math.max(maxnum, Math.max(tmp, tmp1));
        }

        map.put(n, maxnum);
        return maxnum;
    }
}
```
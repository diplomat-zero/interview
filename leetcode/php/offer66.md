```
给定一个数组 A[0,1,…,n-1]，请构建一个数组 B[0,1,…,n-1]，其中 B[i] 的值是数组 A 中除了下标 i 以外的元素的积, 即 B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]。不能使用除法。

示例:
输入: [1,2,3,4,5]
输出: [120,60,40,30,24]
 
提示：
所有元素乘积之和不会溢出 32 位整数
a.length <= 100000
```

```
class Solution {

    /**
     * @param Integer[] $a
     * @return Integer[]
     */
    function constructArr($a) {
        $ret = [];
        if (empty($a)) {
            return $ret;
        }
        $left[0] = 1;
        for ($i = 1; $i < count($a); $i++) {
            $left[$i] = $a[$i - 1] * $left[$i - 1];
        }

        $right[count($a) - 1] = 1;
        for ($j = count($a) - 2; $j >= 0; $j--) {
            $right[$j] = $a[$j + 1] * $right[$j + 1];
        }

        for ($m = 0; $m < count($a); $m++) {
            $ret[$m] = $left[$m] * $right[$m];
        }

        return $ret;
    }
}
```
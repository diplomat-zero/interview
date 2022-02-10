```
写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。

示例:

输入: a = 1, b = 1
输出: 2
 
提示：
a, b 均可能是负数或 0
结果不会溢出 32 位整数
```

```
class Solution {

    /**
     * @param Integer $a
     * @param Integer $b
     * @return Integer
     */
    function add($a, $b) {
        while ($b != 0) {
             $temp = $a ^ $b;
             $b = ($a & $b) << 1;
             $a = $temp;
         }

         return $a;
    }
}
```
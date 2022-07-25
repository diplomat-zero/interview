```
给定两个字符串形式的非负整数 num1 和num2 ，计算它们的和并同样以字符串形式返回。

你不能使用任何內建的用于处理大整数的库（比如 BigInteger）， 也不能直接将输入的字符串转换为整数形式。

 

示例 1：

输入：num1 = "11", num2 = "123"
输出："134"
示例 2：

输入：num1 = "456", num2 = "77"
输出："533"
示例 3：

输入：num1 = "0", num2 = "0"
输出："0"
 

 

提示：

1 <= num1.length, num2.length <= 104
num1 和num2 都只包含数字 0-9
num1 和num2 都不包含任何前导零
```

```

```

```
class Solution {
    public String addStrings(String num1, String num2) {
        int i = num1.length() - 1;
        int j = num2.length() - 1;

        int jin = 0;
        StringBuffer ans = new StringBuffer();
        while (i >= 0 || j >= 0 || jin != 0) {
            int num_a = 0;
            int num_b = 0;
            if (i >= 0) {
                num_a = num1.charAt(i) - '0';
            }
            if (j >= 0) {
                num_b = num2.charAt(j) - '0';
            }
            int value = 0;
            int tmp = num_a + num_b + jin;
            if (tmp >= 10) {
                value = tmp - 10;
                jin = 1;
            } else {
                value = tmp;
                jin = 0;
            }
            ans.append(value);
            i--;
            j--;
        }
        ans.reverse();
        return ans.toString();
    }
}
```
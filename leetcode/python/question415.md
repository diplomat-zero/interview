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
class Solution:
    def addStrings(self, num1: str, num2: str) -> str:
        i = len(num1) - 1
        j = len(num2) - 1
        jin = 0
        res = ''
        while i >= 0 and j >= 0:
            num1_val = int(num1[i])
            num2_val = int(num2[j])
            tmp = num1_val + num2_val + jin
            if tmp >= 10:
                value = tmp - 10
                jin = 1
            else:
                value = tmp
                jin = 0
            res = str(value) + res
            i -= 1
            j -= 1
        
        while i >= 0:
            tmp = int(num1[i]) + jin
            if tmp >= 10:
                value = tmp - 10
                jin = 1
            else:
                value = tmp
                jin = 0
            res = str(value) + res
            i -= 1
        
        while j >= 0:
            tmp = int(num2[j]) + jin
            if tmp >= 10:
                value = tmp - 10
                jin = 1
            else:
                value = tmp
                jin = 0
            res = str(value) + res
            j -= 1
        
        if jin == 1:
            res = '1' + res
        
        return res
```
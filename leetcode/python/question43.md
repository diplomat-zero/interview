```
给定两个以字符串形式表示的非负整数 num1 和 num2，返回 num1 和 num2 的乘积，它们的乘积也表示为字符串形式。

注意：不能使用任何内置的 BigInteger 库或直接将输入转换为整数。

 

示例 1:

输入: num1 = "2", num2 = "3"
输出: "6"
示例 2:

输入: num1 = "123", num2 = "456"
输出: "56088"
 

提示：

1 <= num1.length, num2.length <= 200
num1 和 num2 只能由数字组成。
num1 和 num2 都不包含任何前导零，除了数字0本身。
```

```

```

```
class Solution:
    def multiply(self, num1: str, num2: str) -> str:
        if num1 == "0" or num2 == "0":
            return "0"
        res = [0 for _ in range(len(num1) + len(num2))]
        i = len(num1) - 1
        while i >= 0:
            j = len(num2) - 1
            while j >= 0:
                mul = int(num1[i]) * int(num2[j])
                p1 = i + j
                p2 = i + j + 1
                sum_num = mul + res[p2]
                res[p2] = sum_num % 10
                res[p1] += sum_num // 10
                j -= 1
            i -= 1

        m = 0
        while m < len(res) and res[m] == 0:
            m += 1

        ret = ""
        while m < len(res):
            ret += str(res[m])
            m += 1
        
        return ret
```
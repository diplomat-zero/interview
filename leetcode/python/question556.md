```
给你一个正整数 n ，请你找出符合条件的最小整数，其由重新排列 n 中存在的每位数字组成，并且其值大于 n 。如果不存在这样的正整数，则返回 -1 。

注意 ，返回的整数应当是一个 32 位整数 ，如果存在满足题意的答案，但不是 32 位整数 ，同样返回 -1 。

 

示例 1：

输入：n = 12
输出：21
示例 2：

输入：n = 21
输出：-1
 

提示：

1 <= n <= 231 - 1
```

```

```

```
class Solution:
    def nextGreaterElement(self, n: int) -> int:
        n_str = list(str(n))
        i = len(n_str) - 1
        j = len(n_str) - 2
        
        while j >= 0:
            if n_str[i] <= n_str[j]:
                i -= 1
                j -= 1
            else:
                break
        
        if j < 0:
            return -1
        
        find = j
        last = len(n_str) - 1
        while n_str[last] <= n_str[find]:
            last -= 1

        n_str[last], n_str[find] = n_str[find], n_str[last]

        start = find + 1
        end = len(n_str) - 1
        while start < end:
            n_str[start], n_str[end] = n_str[end], n_str[start]
            start += 1
            end -= 1
        
        res = int("".join(n_str))
        if res >= pow(2, 31):
            return -1
        return res
```
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
class Solution {
    public int nextGreaterElement(int n) {
        char[] num = Integer.toString(n).toCharArray();
        int i = num.length - 2;
        int j = num.length - 1;
        while (i >= 0 && num[i] >= num[j]) {
            i--;
            j--;
        }
        if (i < 0) {
            return -1;
        }
        int k = num.length - 1;
        while (num[i] >= num[k]) {
            k--;
        }

        char tmp = num[i];
        num[i] = num[k];
        num[k] = tmp;

        int left = i + 1;
        int right = num.length - 1;
        while (left < right) {
            char tmp1 = num[left];
            num[left] = num[right];
            num[right] = tmp1;
            left++;
            right--;
        }

        long ans = Long.parseLong(new String(num));
        return ans > Integer.MAX_VALUE ? -1 : (int) ans;
    }
}
```
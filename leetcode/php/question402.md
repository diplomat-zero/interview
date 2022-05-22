```
给你一个以字符串表示的非负整数 num 和一个整数 k ，移除这个数中的 k 位数字，使得剩下的数字最小。请你以字符串形式返回这个最小的数字。

示例 1 ：
输入：num = "1432219", k = 3
输出："1219"
解释：移除掉三个数字 4, 3, 和 2 形成一个新的最小的数字 1219 。

示例 2 ：
输入：num = "10200", k = 1
输出："200"
解释：移掉首位的 1 剩下的数字为 200. 注意输出不能有任何前导零。

示例 3 ：
输入：num = "10", k = 2
输出："0"
解释：从原数字移除所有的数字，剩余为空就是 0 。
 
提示：
1 <= k <= num.length <= 105
num 仅由若干位数字（0 - 9）组成
除了 0 本身之外，num 不含任何前导零
```

```
思路
单调栈

将要入栈元素的元素比当前栈顶元素小 将栈顶元素出栈 将当前元素入栈
```

```
class Solution {

    /**
     * @param String $num
     * @param Integer $k
     * @return String
     */
    function removeKdigits($num, $k) {
        $stack = new SplStack();
        for ($i = 0; $i < strlen($num); $i++) {
            while (!$stack->isEmpty() && $k > 0 && $num[$i] < $stack->top()) {
                $stack->pop();
                $k--;
            }
            if ($num[$i] == 0 && $stack->isEmpty()) {
                continue;
            }
            $stack->push($num[$i]);
        }
        while ($k > 0 && !$stack->isEmpty()) {
            $stack->pop();
            $k--;
        }

        if ($stack->isEmpty()) {
            return '0';
        }

        $res = '';
        while (!$stack->isEmpty()) {
            $res = $stack->pop() . $res;
        }
        return $res;
    }
}
```
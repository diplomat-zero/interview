```
给定一个整数数组 temperatures ，表示每天的温度，返回一个数组 answer ，其中 answer[i] 是指在第 i 天之后，才会有更高的温度。如果气温在这之后都不会升高，请在该位置用 0 来代替。

示例 1:
输入: temperatures = [73,74,75,71,69,72,76,73]
输出: [1,1,4,2,1,1,0,0]

示例 2:
输入: temperatures = [30,40,50,60]
输出: [1,1,1,0]

示例 3:
输入: temperatures = [30,60,90]
输出: [1,1,0]
 
提示：
1 <= temperatures.length <= 105
30 <= temperatures[i] <= 100
```

```
class Solution {

    /**
     * @param Integer[] $temperatures
     * @return Integer[]
     */
    function dailyTemperatures($temperatures) {
        $res = [];
        $stack = new SplStack();
        for ($i = count($temperatures) - 1; $i >= 0; $i--) {
            while (!$stack->isEmpty() && $temperatures[$stack->top()] <= $temperatures[$i]) {
                $stack->pop();
            }

            $res[$i] = $stack->isEmpty() ? 0 : $stack->top() - $i;
            $stack->push($i);
        }

        for ($i = 0; $i < count($res); $i++) {
            $ret[] = $res[$i];
        }
        return $ret;
    }
}
```
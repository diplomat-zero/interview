```

```

```

```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer[]
     */
    function nextGreaterElements($nums) {
        $stack = [];
        $res = [];
        $n = count($nums);
        for ($i = $n * 2 - 1; $i >= 0; $i--) {
            while (!empty($stack) && end($stack) <= $nums[$i % $n]) {
                array_pop($stack);
            }
            $res[$i % $n] = empty($stack) ? -1 : end($stack);
            $stack[] = $nums[$i % $n];
        }
        $ret = [];
        for ($j = 0; $j < count($res); $j++) {
            $ret[] = $res[$j];
        }
        return $ret;
    }
}
```
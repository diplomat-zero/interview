```

```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer[]
     */
    function sortArray($nums) {
        $this->split($nums, 0, count($nums) - 1);
        return $nums;
    }

    function split(&$arr, $left, $right) {
        if ($left >= $right) {
            return;
        }

        $mid = floor(($left + $right) / 2);
        $this->split($arr, $left, $mid);
        $this->split($arr, $mid + 1, $right);

        $this->merge($arr, $left, $mid, $right);
    }

    function merge(&$arr, $left, $mid, $right) {
        $tmp = [];
        $i = $left;
        $j = $mid + 1;

        while ($i <= $mid && $j <= $right) {
            if ($arr[$i] < $arr[$j]) {
                $tmp[] = $arr[$i];
                $i++;
            } else {
                $tmp[] = $arr[$j];
                $j++;
            } 
        }

        while ($i <= $mid) {
            $tmp[] = $arr[$i];
            $i++;
        }

        while ($j <= $right) {
            $tmp[] = $arr[$j];
            $j++;
        }

        for ($k = 0; $k < count($tmp); $k++) {
            $arr[$left + $k] = $tmp[$k];
        }
    }
}
```
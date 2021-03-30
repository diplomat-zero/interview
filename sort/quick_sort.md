```
    function quickSort(&$nums, $start, $end)
    {
        $find = $this->find($nums, $start, $end);
        if ($start < $find - 1) {
            $this->quickSort($nums, $start, $find - 1);
        }
        if ($find + 1 < $end) {
            $this->quickSort($nums, $find + 1, $end);
        }

    }

    function find(&$nums, $start, $end)
    {
        $target = $nums[$start];
        while ($start < $end) {
            while ($start < $end && $nums[$end] >= $target) {
                $end--;
            }
            $nums[$start] = $nums[$end];
            while ($start < $end && $nums[$start] <= $target) {
                $start++;
            }
            $nums[$end] = $nums[$start];
        }
        $nums[$end] = $target;
        return $end;
    }
```
```
在未排序的数组中找到第k个最大的元素。请注意，你需要找的是数组排序后的第k个最大的元素，而不是第k个不同的元素。

示例 1:
输入: [3,2,1,5,6,4] 和 k = 2
输出: 5

示例 2:
输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4

说明:
你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $k
     * @return Integer
     */
    function findKthLargest($nums, $k) {
        return $this->quick($nums, 0, count($nums) - 1, $k);
    }

    function quick(&$nums, $left, $right, $k)
    {
        if($left >= $right){
            return $nums[$left];
        }

        $find = $this->choose($nums, $left, $right);

        if (count($nums) - $k == $find) {
            return $nums[$find];
        } elseif ($find > count($nums) - $k) {
            return $this->quick($nums, $left, $find - 1, $k);
        } else {
            return $this->quick($nums, $find + 1, $right, $k);
        }
    }

    function choose(&$nums, $left, $right)
    {
        $target = $nums[$left];
        while ($left < $right) {
            while ($left < $right && $nums[$right] >= $target) {
                $right--;
            }
            $nums[$left] = $nums[$right];
            while ($left < $right && $nums[$left] <= $target) {
                $left++;
            }
            $nums[$right] = $nums[$left];
        }

        $nums[$right] = $target;
        return $right;
    }
}
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $k
     * @return Integer
     */
    function findKthLargest($nums, $k) {
        $head = new SplMinHeap();
        for ($i = 0; $i < count($nums); $i++) {
            if ($head->count() < $k) {
                $head->insert($nums[$i]);
            } else {
                if ($head->top() < $nums[$i]) {
                    $head->extract();
                    $head->insert($nums[$i]);
                }
            }
        }

        return $head->top();
    }
}
```
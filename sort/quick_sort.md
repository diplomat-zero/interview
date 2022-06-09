```
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer[]
     */
    function sortArray($nums) {
        $this->quickSort($nums, 0, count($nums) - 1);
        return $nums;
    }

    function quickSort(&$nums, $start, $end) {
        if ($start < $end) {
            $find = $this->find($nums, $start, $end);
            $this->quickSort($nums, $start, $find - 1);
            $this->quickSort($nums, $find + 1, $end);
        }
    }

    function find(&$arr, $start, $end) {
        $target = $arr[$start];
        while ($start < $end) {
            while ($start < $end && $arr[$end] >= $target) {
                $end--;
            }
            $this->swap($arr, $start, $end);
            while ($start < $end && $arr[$start] <= $target) {
                $start++;
            }
            $this->swap($arr, $start, $end);
        }
        return $start;
    }

    function swap(&$nums, $a, $b) {
        $tmp = $nums[$a];
        $nums[$a] = $nums[$b];
        $nums[$b] = $tmp;
    }
}
```

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

```
class Solution:
    def sortArray(self, nums: List[int]) -> List[int]:
        self.quickSort(nums, 0, len(nums) - 1)
        return nums

    def quickSort(self, nums, start, end):
        if start < end:
            find = self.findNum(nums, start, end)
            self.quickSort(nums, start, find - 1)
            self.quickSort(nums, find + 1, end)

    def findNum(self, nums, start, end):
        target = nums[start]
        while start < end :
            while start < end and target <= nums[end]:
                end -= 1
            nums[start],nums[end] = nums[end], nums[start]
            while start < end and target >= nums[start]:
                start += 1
            nums[start],nums[end] = nums[end], nums[start]
        return start
```
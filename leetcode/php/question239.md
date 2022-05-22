```
给你一个整数数组 nums，有一个大小为 k 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 k 个数字。滑动窗口每次只向右移动一位。

返回 滑动窗口中的最大值 。

示例 1：
输入：nums = [1,3,-1,-3,5,3,6,7], k = 3
输出：[3,3,5,5,6,7]
解释：
滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7

示例 2：
输入：nums = [1], k = 1
输出：[1]
 
提示：
1 <= nums.length <= 105
-104 <= nums[i] <= 104
1 <= k <= nums.length
```

```
思路
单调队列

```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $k
     * @return Integer[]
     */
    function maxSlidingWindow($nums, $k) {
        $my_queue = new MyQueue1();
        $res = [];
        for ($i = 0; $i < count($nums); $i++) {
            if ($i < $k - 1) {
                $my_queue->addLast($nums[$i]);
            } else {
                $my_queue->addLast($nums[$i]);
                $res[] = $my_queue->getMax();
                $my_queue->moveFirst($nums[$i - $k + 1]);
            }
        }
        return $res;
    }
}
class MyQueue1 {
    public $queue;
    function __construct() {
        $this->queue = new SplQueue();
    }

    function addLast($num) {
        while (!$this->queue->isEmpty() && $this->queue->top() < $num) {
            $this->queue->pop();
        }
        $this->queue->enqueue($num);
    }

    function getMax() {
        return $this->queue->bottom();
    }

    function moveFirst($num) {
        if ($this->queue->bottom() == $num) {
            $this->queue->dequeue();
        }
    }
}
class MyQueue {
    public $num;

    function addLast($nums) {
        while (!empty($this->num) && end($this->num) < $nums) {
            array_pop($this->num);
        }
        $this->num[] = $nums;
    }

    function getMax() {
        return $this->num[0];
    }

    function moveFirst($n) {
        if ($n == $this->num[0]) {
            array_shift($this->num);
        }
    }
}
```
```
中位数是有序列表中间的数。如果列表长度是偶数，中位数则是中间两个数的平均值。
例如，
[2,3,4] 的中位数是 3
[2,3] 的中位数是 (2 + 3) / 2 = 2.5
设计一个支持以下两种操作的数据结构：
void addNum(int num) - 从数据流中添加一个整数到数据结构中。
double findMedian() - 返回目前所有元素的中位数。

示例：
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2

进阶:
如果数据流中所有整数都在 0 到 100 范围内，你将如何优化你的算法？
如果数据流中 99% 的整数都在 0 到 100 范围内，你将如何优化你的算法？
```

```
class MedianFinder {
    /**
     */
    private $small;
    private $big;
    function __construct() {
        $this->small = new SplMinHeap;
        $this->big = new SplMaxHeap;
    }

    /**
     * @param Integer $num
     * @return NULL
     */
    function addNum($num) {
        if ($this->small->count() == 0) {
            $this->small->insert($num);
            return;
            }
        if ($this->small->count() == $this->big->count()) {
            $this->small->insert($num);
            if ($this->small->top() < $this->big->top()) {
                $this->big->insert($this->small->extract());
            }
        } elseif ($this->small->count() > $this->big->count()) {
            $this->big->insert($num);
            if ($this->small->top() < $this->big->top()) {
                $this->big->insert($this->small->extract());
                $this->small->insert($this->big->extract());
            }
        } else {
            $this->small->insert($num);
            if ($this->small->top() < $this->big->top()) {
                $this->big->insert($this->small->extract());
                $this->small->insert($this->big->extract());
            }
        }
    }

    /**
     * @return Float
     */
    function findMedian() {
        if ($this->small->count() > $this->big->count()) {
            return $this->small->top();
        } else if ($this->small->count() < $this->big->count()){
            return $this->big->top();
        } else {
            return ($this->small->top() + $this->big->top()) / 2;
        }
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * $obj = MedianFinder();
 * $obj->addNum($num);
 * $ret_2 = $obj->findMedian();
 */
```
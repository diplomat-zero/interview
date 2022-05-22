```
设计一个支持 push ，pop ，top 操作，并能在常数时间内检索到最小元素的栈。

push(x) —— 将元素 x 推入栈中。
pop() —— 删除栈顶的元素。
top() —— 获取栈顶元素。
getMin() —— 检索栈中的最小元素。
 
示例:

输入：
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

输出：
[null,null,null,null,-3,null,0,-2]

解释：
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2.
 
提示：

pop、top 和 getMin 操作总是在 非空栈 上调用。
```

```
思路
辅助栈

这道题最直接的解法就是我们可以用两个栈，一个栈去保存正常的入栈出栈的值，另一个栈去存最小值，也就是用栈顶保存当前所有元素的最小值。存最小值的栈的具体操作流程如下：
将第一个元素入栈。
新加入的元素如果大于栈顶元素，那么新加入的元素就不处理。
新加入的元素如果小于等于栈顶元素，那么就将新元素入栈。
出栈元素不等于栈顶元素，不操作。
出栈元素等于栈顶元素，那么就将栈顶元素出栈。
```

```
class MinStack {
    /**
     */
    public $stack;
    public $min_stack;
    function __construct() {
        $this->stack = new SplStack();
        $this->min_stack = new SplStack();
    }

    /**
     * @param Integer $val
     * @return NULL
     */
    function push($val) {
        $this->stack->push($val);
        if ($this->min_stack->isEmpty() || $val <= $this->min_stack->top()) {
            $this->min_stack->push($val);
        }
    }

    /**
     * @return NULL
     */
    function pop() {
        $ret = $this->stack->pop();
        if ($ret == $this->min_stack->top()) {
            $this->min_stack->pop();
        }
    }

    /**
     * @return Integer
     */
    function top() {
        return $this->stack->top();
    }

    /**
     * @return Integer
     */
    function getMin() {
        return $this->min_stack->top();
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * $obj = MinStack();
 * $obj->push($val);
 * $obj->pop();
 * $ret_3 = $obj->top();
 * $ret_4 = $obj->getMin();
 */
```

```
class MinStack {
    public $arr;
    /**
     * initialize your data structure here.
     */
    function __construct() {
        $this->arr = [];
    }

    /**
     * @param Integer $x
     * @return NULL
     */
    function push($x) {
        array_unshift($this->arr, $x);
    }

    /**
     * @return NULL
     */
    function pop() {
        array_shift($this->arr);
    }

    /**
     * @return Integer
     */
    function top() {
        return reset($this->arr);
    }

    /**
     * @return Integer
     */
    function getMin() {
        return min($this->arr);
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * $obj = MinStack();
 * $obj->push($x);
 * $obj->pop();
 * $ret_3 = $obj->top();
 * $ret_4 = $obj->getMin();
 */
```
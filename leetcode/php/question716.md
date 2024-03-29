```
设计一个最大栈数据结构，既支持栈操作，又支持查找栈中最大元素。

实现 MaxStack 类：

MaxStack() 初始化栈对象
void push(int x) 将元素 x 压入栈中。
int pop() 移除栈顶元素并返回这个元素。
int top() 返回栈顶元素，无需移除。
int peekMax() 检索并返回栈中最大元素，无需移除。
int popMax() 检索并返回栈中最大元素，并将其移除。如果有多个最大元素，只要移除 最靠近栈顶 的那个。
 

示例：

输入
["MaxStack", "push", "push", "push", "top", "popMax", "top", "peekMax", "pop", "top"]
[[], [5], [1], [5], [], [], [], [], [], []]
输出
[null, null, null, null, 5, 5, 1, 5, 1, 5]

解释
MaxStack stk = new MaxStack();
stk.push(5);   // [5] - 5 既是栈顶元素，也是最大元素
stk.push(1);   // [5, 1] - 栈顶元素是 1，最大元素是 5
stk.push(5);   // [5, 1, 5] - 5 既是栈顶元素，也是最大元素
stk.top();     // 返回 5，[5, 1, 5] - 栈没有改变
stk.popMax();  // 返回 5，[5, 1] - 栈发生改变，栈顶元素不再是最大元素
stk.top();     // 返回 1，[5, 1] - 栈没有改变
stk.peekMax(); // 返回 5，[5, 1] - 栈没有改变
stk.pop();     // 返回 1，[5] - 此操作后，5 既是栈顶元素，也是最大元素
stk.top();     // 返回 5，[5] - 栈没有改变
 

提示：

-107 <= x <= 107
最多调用 104 次 push、pop、top、peekMax 和 popMax
调用 pop、top、peekMax 或 popMax 时，栈中 至少存在一个元素
 

进阶： 

试着设计解决方案：调用 top 方法的时间复杂度为 O(1) ，调用其他方法的时间复杂度为 O(logn) 。 
```

```

```

```
class MaxStack {
    /**
     */
    public $stack1;
    public $stack2;
    function __construct() {
        $this->stack1 = new SplStack();
        $this->stack2 = new SplStack();
    }

    /**
     * @param Integer $x
     * @return NULL
     */
    function push($x) {
        $this->stack1->push($x);
        if ($this->stack2->isEmpty()) {
            $this->stack2->push($x);
        } else {
            $max = $this->stack2->top();
            if ($max > $x) {
                $this->stack2->push($max);
            } else {
                $this->stack2->push($x);
            }
        }
    }

    /**
     * @return Integer
     */
    function pop() {
        $end = $this->stack1->pop();
        $this->stack2->pop();
        return $end;
    }

    /**
     * @return Integer
     */
    function top() {
        return $this->stack1->top();
    }

    /**
     * @return Integer
     */
    function peekMax() {
        return $this->stack2->top();
    }

    /**
     * @return Integer
     */
    function popMax() {
        $max = $this->peekMax();
        while ($this->top() != $max) {
            $buffer[] = $this->pop();
        }
        $this->pop();
        while (!empty($buffer)) {
            $this->push(end($buffer));
            array_pop($buffer);
        }

        return $max;
    }
}

/**
 * Your MaxStack object will be instantiated and called as such:
 * $obj = MaxStack();
 * $obj->push($x);
 * $ret_2 = $obj->pop();
 * $ret_3 = $obj->top();
 * $ret_4 = $obj->peekMax();
 * $ret_5 = $obj->popMax();
 */
 ```
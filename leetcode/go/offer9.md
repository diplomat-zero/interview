```
用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

 

示例 1：

输入：
["CQueue","appendTail","deleteHead","deleteHead","deleteHead"]
[[],[3],[],[],[]]
输出：[null,null,3,-1,-1]
示例 2：

输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
提示：

1 <= values <= 10000
最多会对 appendTail、deleteHead 进行 10000 次调用
```

```

```

```
type CQueue struct {
    in_stack []int
    out_stack []int
}


func Constructor() CQueue {
    return CQueue{in_stack: []int{}, out_stack: []int{}}
}


func (this *CQueue) AppendTail(value int)  {
    this.in_stack = append(this.in_stack, value)
}


func (this *CQueue) DeleteHead() int {
    if len(this.in_stack) == 0 && len(this.out_stack) == 0 {
        return -1
    }
    if len(this.out_stack) != 0 {
        ret := this.out_stack[len(this.out_stack) - 1]
        this.out_stack = this.out_stack[:len(this.out_stack) - 1]
        return ret
    }
    for len(this.in_stack) > 0 {
        this.out_stack = append(this.out_stack, this.in_stack[len(this.in_stack) - 1])
        this.in_stack = this.in_stack[:len(this.in_stack) - 1]
    }
    ret := this.out_stack[len(this.out_stack) - 1]
    this.out_stack = this.out_stack[:len(this.out_stack) - 1]
    return ret
}


/**
 * Your CQueue object will be instantiated and called as such:
 * obj := Constructor();
 * obj.AppendTail(value);
 * param_2 := obj.DeleteHead();
 */
```
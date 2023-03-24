```
请你设计并实现一个满足  LRU (最近最少使用) 缓存 约束的数据结构。
实现 LRUCache 类：
LRUCache(int capacity) 以 正整数 作为容量 capacity 初始化 LRU 缓存
int get(int key) 如果关键字 key 存在于缓存中，则返回关键字的值，否则返回 -1 。
void put(int key, int value) 如果关键字 key 已经存在，则变更其数据值 value ；如果不存在，则向缓存中插入该组 key-value 。如果插入操作导致关键字数量超过 capacity ，则应该 逐出 最久未使用的关键字。
函数 get 和 put 必须以 O(1) 的平均时间复杂度运行。

 

示例：

输入
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
输出
[null, null, null, 1, null, -1, null, -1, 3, 4]

解释
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // 缓存是 {1=1}
lRUCache.put(2, 2); // 缓存是 {1=1, 2=2}
lRUCache.get(1);    // 返回 1
lRUCache.put(3, 3); // 该操作会使得关键字 2 作废，缓存是 {1=1, 3=3}
lRUCache.get(2);    // 返回 -1 (未找到)
lRUCache.put(4, 4); // 该操作会使得关键字 1 作废，缓存是 {4=4, 3=3}
lRUCache.get(1);    // 返回 -1 (未找到)
lRUCache.get(3);    // 返回 3
lRUCache.get(4);    // 返回 4
 

提示：

1 <= capacity <= 3000
0 <= key <= 10000
0 <= value <= 105
最多调用 2 * 105 次 get 和 put
```

```

```

```
type LRUCache struct {
    capacity int
    kmap map[int]*Node
    cache *DoubleList
}


func Constructor(capacity int) LRUCache {
    return LRUCache {
        capacity: capacity,
        kmap: map[int]*Node{},
        cache: initDoubleList(),
    }
}


func (this *LRUCache) Get(key int) int {
    node,ok := this.kmap[key]
    if !ok {
        return -1
    }
    this.makeRecently(key)
    return node.val
}


func (this *LRUCache) Put(key int, value int)  {
    _,ok := this.kmap[key]
    if ok {
        this.deleteKey(key)
        this.addRecently(key, value)
    } else {
        if this.cache.size == this.capacity {
            this.removeLeastRecently()
        }
        this.addRecently(key, value)
    }
}

func (this *LRUCache) makeRecently(key int) {
    node := this.kmap[key]
    this.cache.remove(node)
    this.cache.addLast(node)
}

func (this *LRUCache) addRecently(key int, value int) {
    node := initNode(key, value)
    this.kmap[key] = node
    this.cache.addLast(node)
}

func (this *LRUCache) deleteKey(key int) {
    node := this.kmap[key]
    this.cache.remove(node)
    delete(this.kmap, key)
}

func (this *LRUCache) removeLeastRecently() {
    first := this.cache.removeFirst()
    delete(this.kmap, first.key)
}

type Node struct {
    key int
    val int
    prev *Node
    next *Node
}

func initNode(key int, val int) *Node {
    return &Node{
        key: key,
        val: val,
    }
}

type DoubleList struct {
    head *Node
    tail *Node
    size int
}

func initDoubleList() *DoubleList {
    ddl := &DoubleList{
        head: initNode(0,0),
        tail: initNode(0,0),
        size: 0,
    }
    ddl.head.next = ddl.tail
    ddl.tail.prev = ddl.head
    return ddl
}

func (this *DoubleList) addLast(x *Node) {
    x.prev = this.tail.prev
    x.next = this.tail
    this.tail.prev.next = x
    this.tail.prev = x
    this.size++
}

func (this *DoubleList) remove(x *Node) {
    x.prev.next = x.next
    x.next.prev = x.prev
    x.next = nil
    x.prev = nil
    this.size--
}

func (this *DoubleList) removeFirst() *Node {
    if this.head.next == this.tail {
        return nil
    }
    first := this.head.next
    this.remove(first)
    return first
}


/**
 * Your LRUCache object will be instantiated and called as such:
 * obj := Constructor(capacity);
 * param_1 := obj.Get(key);
 * obj.Put(key,value);
 */
```
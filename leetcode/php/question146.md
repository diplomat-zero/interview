```
请你设计并实现一个满足  LRU (最近最少使用) 缓存 约束的数据结构。
实现 LRUCache 类：
LRUCache(int capacity) 以 正整数 作为容量 capacity 初始化 LRU 缓存
int get(int key) 如果关键字 key 存在于缓存中，则返回关键字的值，否则返回 -1 。
void put(int key, int value) 如果关键字 key 已经存在，则变更其数据值 value ；如果不存在，则向缓存中插入该组 key-value 。如果插入操作导致关键字数量超过 capacity ，则应该 逐出 最久未使用的关键字。
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
class LRUCache {
    /**
     * @param Integer $capacity
     */
    public $cache;
    public $map;
    public $cap;
    function __construct($capacity) {
        $this->cap = $capacity;
        $this->cache = new DoubleList();
        $this->map = [];
    }

    /**
     * @param Integer $key
     * @return Integer
     */
    function get($key) {
        if (!isset($this->map[$key])) {
            return -1;
        }

        $this->makeRecently($key);
        return $this->map[$key]->value;
    }

    /**
     * @param Integer $key
     * @param Integer $value
     * @return NULL
     */
    function put($key, $value) {
        if (isset($this->map[$key])) {
            $this->deleteKey($key);
            $this->addRecently($key, $value);
        } else {
            if ($this->cache->size() == $this->cap) {
                $this->removeLeastRecently();
            } 
            $this->addRecently($key, $value);
        }
    }

    function makeRecently($key) {
        $node = $this->map[$key];

        $this->cache->remove($node);
        $this->cache->addLast($node);
    }

    function addRecently($key, $value) {
        $node = new Node($key, $value);
        $this->map[$key] = $node;
        $this->cache->addLast($node);
    }

    function deleteKey($key) {
        $node = $this->map[$key];

        unset($this->map[$key]);
        $this->cache->remove($node);
    }

    function removeLeastRecently() {
        $node = $this->cache->removeFirst();
        unset($this->map[$node->key]);
    }
}
class Node {
    public $key;
    public $value;
    public $next;
    public $prev;
    function __construct($key, $value, $next = NULL, $prev = NULL) {
        $this->key = $key;
        $this->value = $value;
        $this->next = $next;
        $this->prev = $prev;
    }
}

class DoubleList {
    public $head;
    public $tail;
    public $size;

    function __construct() {
        $this->head = new Node(0,0);
        $this->tail = new Node(0,0);
        $this->head->next = $this->tail;
        $this->tail->prev = $this->head;
        $this->size = 0;
    }

    function addLast($x) {
        $x->prev = $this->tail->prev;
        $x->next = $this->tail;
        $this->tail->prev->next = $x;
        $this->tail->prev = $x;
        $this->size++;
    }

    function remove($x) {
        $x->prev->next = $x->next;
        $x->next->prev = $x->prev;
        $this->size--;
    }

    function removeFirst() {
        if ($this->head->next == $this->tail) {
            return NULL;
        }
        $first = $this->head->next;
        $this->remove($first);
        return $first;
    }

    function size() {
        return $this->size;
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * $obj = LRUCache($capacity);
 * $ret_1 = $obj->get($key);
 * $obj->put($key, $value);
 */
 ```
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
class LRUCache:

    def __init__(self, capacity: int):
        self.cache = DoubleList()
        self.map = {}
        self.cap = capacity

    def get(self, key: int) -> int:
        if key not in self.map:
            return -1
        self.makeRecently(key)
        return self.map[key].value

    def put(self, key: int, value: int) -> None:
        if key in self.map:
            self.deleteKey(key)
            self.addRecently(key, value)
        else:
            len = self.cache.cacheSize()
            if len == self.cap:
                self.removeLeastRecenlty()
            self.addRecently(key, value)
    
    def makeRecently(self, key):
        node = self.map[key]
        self.cache.remove(node)
        self.cache.addLast(node)

    def addRecently(self, key, value):
        node = Node(key, value)

        self.map[key] = node
        self.cache.addLast(node)

    def deleteKey(self, key):
        node = self.map[key]

        del(self.map[key])
        self.cache.remove(node)

    def removeLeastRecenlty(self):
        node = self.cache.removeFirst()

        del(self.map[node.key])

class Node:
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.next = None
        self.prev = None


class DoubleList:
    def __init__(self):
        self.head = Node(0, 0)
        self.tail = Node(0, 0)
        self.head.next = self.tail
        self.tail.prev = self.head
        self.size = 0
    
    def addLast(self, x):
        x.next = self.tail
        x.prev = self.tail.prev
        self.tail.prev.next = x
        self.tail.prev = x
        self.size += 1
        
    def remove(self, x):
        x.prev.next = x.next
        x.next.prev = x.prev
        self.size -= 1
        
    def removeFirst(self):
        if self.head.next == self.tail:
            return None
        first = self.head.next
        self.remove(first)
        return first
    
    def cacheSize(self):
        return self.size


# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```
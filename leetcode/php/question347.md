```
给你一个整数数组 nums 和一个整数 k ，请你返回其中出现频率前 k 高的元素。你可以按 任意顺序 返回答案。

示例 1:
输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]

示例 2:
输入: nums = [1], k = 1
输出: [1]
 
提示：
1 <= nums.length <= 105
k 的取值范围是 [1, 数组中不相同的元素的个数]
题目数据保证答案唯一，换句话说，数组中前 k 个高频元素的集合是唯一的
 
进阶：你所设计算法的时间复杂度 必须 优于 O(n log n) ，其中 n 是数组大小。
```

```

```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $k
     * @return Integer[]
     */
    function topKFrequent($nums, $k) {
        $map = [];
        for ($i = 0; $i < count($nums); $i++) {
            if (isset($map[$nums[$i]])) {
                $map[$nums[$i]]++;
            } else {
                $map[$nums[$i]] = 1;
            }
        }
        $heap = new MyHeap();
        foreach ($map as $key => $value) {
            if ($heap->count() < $k) {
                $heap->insert([$key, $value]);
            } else {
                if ($heap->top()[1] < $value) {
                    $heap->extract();
                    $heap->insert([$key, $value]);
                }
            }
        }
        $ret = [];
        while (!$heap->isEmpty()) {
            $ret[] = $heap->extract()[0];
        }
        return $ret;
    }
}
class MyHeap extends SplMinHeap {
    protected function compare($value1, $value2)
    {
        return $value2[1] - $value1[1];
    }
}
```
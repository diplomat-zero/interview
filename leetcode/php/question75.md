```
给定一个包含红色、白色和蓝色，一共n个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。
此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。

示例 1：
输入：nums = [2,0,2,1,1,0]
输出：[0,0,1,1,2,2]

示例 2：
输入：nums = [2,0,1]
输出：[0,1,2]

示例 3：
输入：nums = [0]
输出：[0]

示例 4：
输入：nums = [1]
输出：[1]
 
提示：

n == nums.length
1 <= n <= 300
nums[i] 为 0、1 或 2
 
进阶：
你可以不使用代码库中的排序函数来解决这道题吗？
你能想出一个仅使用常数空间的一趟扫描算法吗？
```

```
// all in [0, zero) = 0
// all in [zero, i) = 1
// all in [two, len - 1] = 2
        
// 循环终止条件是 i == two，那么循环可以继续的条件是 i < two
// 为了保证初始化的时候 [0, zero) 为空，设置 zero = 0，
// 所以下面遍历到 0 的时候，先交换，再加
int zero = 0;

// 为了保证初始化的时候 [two, len - 1] 为空，设置 two = len
// 所以下面遍历到 2 的时候，先减，再交换
int two = len;
int i = 0;
// 当 i == two 上面的三个子区间正好覆盖了全部数组
// 因此，循环可以继续的条件是 i < two
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return NULL
     */
    function sortColors(&$nums) {
        $zero = 0;
        $two = count($nums);
        $i = 0;
        while ($i < $two) {
            if ($nums[$i] == 0) {
                $this->swap($nums, $i, $zero);
                $zero++;
                $i++;
            } else if ($nums[$i] == 1) {
                $i++;
            } else {
                $two--;
                $this->swap($nums, $i, $two);
            }
        }
    }

    function swap(&$nums, $a, $b) {
        $tmp = $nums[$a];
        $nums[$a] = $nums[$b];
        $nums[$b] = $tmp;
    }
}
```

```
第一次遍历将所有的0换到头部。
第二次遍历将所有的1换到0之后。
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return NULL
     */
    function sortColors(&$nums) {
        $len = count($nums);
        $pre = 0;
        for ($i = 0; $i < $len; $i++) {
            if ($nums[$i] == 0) {
                $this->swap($nums, $i, $pre);
                $pre++;
            }
        }

        for ($i = $pre; $i < $len; $i++) {
            if ($nums[$i] == 1) {
                $this->swap($nums, $i, $pre);
                $pre++;
            }
        }
    }

    function swap(&$nums, $a, $b) {
        $tmp = $nums[$a];
        $nums[$a] = $nums[$b];
        $nums[$b] = $tmp;
    }
}
```
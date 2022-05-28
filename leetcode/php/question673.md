```
给定一个未排序的整数数组 nums ， 返回最长递增子序列的个数 。
注意 这个数列必须是 严格 递增的。

示例 1:
输入: [1,3,5,4,7]
输出: 2
解释: 有两个最长递增子序列，分别是 [1, 3, 4, 7] 和[1, 3, 5, 7]。

示例 2:
输入: [2,2,2,2,2]
输出: 5
解释: 最长递增子序列的长度是1，并且存在5个子序列的长度为1，因此输出5。
 
提示: 
1 <= nums.length <= 2000
-106 <= nums[i] <= 106
```

```
定义状态
dp[i]：到nums[i]为止的最长递增子序列长度
count[i]：到nums[i]为止的最长递增子序列个数
初始化状态
dp = [1] * n：代表最长递增子序列的长度至少为1
count = [1] * n：代表最长递增子序列的个数至少为1
状态转移
对于每一个数nums[i]，看在它之前的数nums[j](0<= j < i)是否比当前数nums[i]小，如果nums[i] > nums[j]，那么相当于到nums[j]为止的最长递增子序列长度到nums[i]增加了1，到nums[i]为止的最长递增子序列长度就变成了dp[i] = dp[j] + 1；但是因为满足nums[i] > nums[j] 的nums[j]不止一个，dp[i]应该取这些dp[j] + 1的最大值，并且这些dp[j] + 1还会有相等的情况，一旦相等，到nums[i]为止的最长递增子序列个数就应该增加了。因此，具体的状态转移如下，在nums[i] > nums[j]的大前提下：
如果dp[j] + 1 > dp[i]，说明最长递增子序列的长度增加了，dp[i] = dp[j] + 1，长度增加，数量不变 count[i] = count[j]
如果dp[j] + 1 == dp[i]，说明最长递增子序列的长度并没有增加，但是出现了长度一样的情况，数量增加 count[i] += count[j]
记录最长递增子序列的最大长度max_length
遍历dp数组，如果dp数组记录的最大长度dp[i]等于max_length，将对应的数量count[i]加到结果res中
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function findNumberOfLIS($nums) {
        $max = 1;
        $dp = array_fill(0, count($nums), 1);
        $dp1 = array_fill(0, count($nums), 1);
        for ($i = 0; $i < count($nums); $i++) {
            for ($j = 0; $j < $i; $j++) {
                if ($nums[$j] < $nums[$i]) {
                    if ($dp[$i] == $dp[$j] + 1) {
                        $dp1[$i] += $dp1[$j];
                    } elseif ($dp[$i] < $dp[$j] + 1) {
                        $dp1[$i] = $dp1[$j];
                    }
                    $dp[$i] = max($dp[$i], $dp[$j] + 1);
                    $max = max($max, $dp[$i]);
                }
            }
        }
        $count = 0;
        for ($m = 0; $m < count($dp); $m++) {
            if ($dp[$m] == $max) {
                $count += $dp1[$m];
            }
        }
        return $count;
    }
}
```
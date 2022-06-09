```
给你一个长度为 n 的整数数组 nums ，其中 nums 的所有整数都在范围 [1, n] 内，且每个整数出现 一次 或 两次 。请你找出所有出现 两次 的整数，并以数组形式返回。

你必须设计并实现一个时间复杂度为 O(n) 且仅使用常量额外空间的算法解决此问题。

示例 1：
输入：nums = [4,3,2,7,8,2,3,1]
输出：[2,3]

示例 2：
输入：nums = [1,1,2]
输出：[1]

示例 3：
输入：nums = [1]
输出：[]
 
提示：
n == nums.length
1 <= n <= 105
1 <= nums[i] <= n
nums 中的每个元素出现 一次 或 两次
```

```
由于数组 nums 的长度是 n，下标范围是 [0,n−1]，每个元素都在范围 [1,n] 内，因此可以将数组看成哈希表，利用数组下标的信息表示每个整数是否出现两次。对于下标 index，满足 0 ≤ index < n，1 ≤ index+1 ≤ n，nums[index] 可以用于表示整数 index+1 是否出现两次。

遍历数组 nums。对于元素 num，其对应的下标为 index=∣num∣−1，根据 nums[index] 的正负性执行如下操作：

如果 nums[index]>0，则将 nums[index] 的值更新为其相反数；

如果 nums[index]<0，则 ∣nums∣=index+1 是出现两次的整数，将其添加到结果中。

上述做法的原理如下：

初始时数组 nums 中的整数都是正数，表示尚未被访问；

当一个整数被访问时，如果该整数对应的下标处的元素是正数，则该整数尚未被访问，因此将该整数对应的下标处的元素改成其相反数，相反数是负数，表示被访问了一次；

当一个整数被访问时，如果该整数对应的下标处的元素是负数，则该整数已经被访问，因此该整数被第二次访问，即该整数是出现两次的整数。

需要注意的是，遍历数组 nums 的过程中，遍历到的元素 num 可能已经被改成负数，因此在计算下标 index 时需要对 num 取绝对值然后减 1。
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer[]
     */
    function findDuplicates($nums) {
        $res = [];
        for ($i = 0; $i < count($nums); $i++) {
            $num = $nums[$i];
            $index = abs($num) - 1;
            if ($nums[$index] > 0) {
                $nums[$index] = -$nums[$index];
            } else {
                $res[] = $index + 1;
            }
        }
        return $res;
    }
}
```
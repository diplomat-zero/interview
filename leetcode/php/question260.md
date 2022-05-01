```
给定一个整数数组 nums，其中恰好有两个元素只出现一次，其余所有元素均出现两次。 找出只出现一次的那两个元素。你可以按 任意顺序 返回答案。
进阶：你的算法应该具有线性时间复杂度。你能否仅使用常数空间复杂度来实现？

示例 1：
输入：nums = [1,2,1,3,2,5]
输出：[3,5]
解释：[5, 3] 也是有效的答案。

示例 2：
输入：nums = [-1,0]
输出：[-1,0]

示例 3：
输入：nums = [0,1]
输出：[1,0]

提示：
2 <= nums.length <= 3 * 104
-231 <= nums[i] <= 231 - 1
除两个只出现一次的整数外，nums 中的其他数字都出现两次
```

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer[]
     */
    function singleNumber($nums) {
        $xor = 0;
        foreach ($nums as $value) {
            $xor = $xor ^ $value;
        }

        $lsb = $xor & (-$xor);

        $ret1 = $ret2 = 0;
        foreach ($nums as $value1) {
            if (($value1 & $lsb) == 0) {
                $ret1 = $ret1 ^ $value1;
            } else {
                $ret2 = $ret2 ^ $value1;
            }
        }

        return [$ret1, $ret2];
    }
}
```
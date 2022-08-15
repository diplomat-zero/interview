```
给你一个整数数组 nums，请你将该数组升序排列。

 

示例 1：

输入：nums = [5,2,3,1]
输出：[1,2,3,5]
示例 2：

输入：nums = [5,1,1,2,0,0]
输出：[0,0,1,1,2,5]
 

提示：

1 <= nums.length <= 5 * 104
-5 * 104 <= nums[i] <= 5 * 104
```

```

```

```
class Solution {
    public int[] sortArray(int[] nums) {
        quickSort(nums, 0, nums.length - 1);
        return nums;
    }

    public void quickSort(int[] nums, int left, int right) {
        if (left < right) {
            int find_num = find(nums, left, right);
            quickSort(nums, left, find_num - 1);
            quickSort(nums, find_num + 1, right);
        }
    }

    public int find(int[] nums, int left, int right) {
        int target = nums[left];
        while (left < right) {
            while (left < right && nums[right] >= target) {
                right--;
            }
            swap(nums, left, right);
            while (left < right && nums[left] <= target) {
                left++;
            }
            swap(nums, left, right);
        }
        
        return left;
    }

    public void swap(int[] nums, int left, int right) {
        int tmp = nums[left];
        nums[left] = nums[right];
        nums[right] = tmp;
    }
}
```
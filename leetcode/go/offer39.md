```
数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

 

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

 

示例 1:

输入: [1, 2, 3, 2, 2, 2, 5, 4, 2]
输出: 2
 

限制：

1 <= 数组长度 <= 50000
```

```

```

```
func majorityElement(nums []int) int {
    major := nums[0]
    count := 1
    for _,value := range nums {
        if value == major {
            count++
        } else {
            count--
            if count == 0 {
                major = value
                count++
            }
        }
    }
    return major
}
```
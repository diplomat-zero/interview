```
给你一个整数数组 arr，只有可以将其划分为三个和相等的 非空 部分时才返回 true，否则返回 false。

形式上，如果可以找出索引 i + 1 < j 且满足 (arr[0] + arr[1] + ... + arr[i] == arr[i + 1] + arr[i + 2] + ... + arr[j - 1] == arr[j] + arr[j + 1] + ... + arr[arr.length - 1]) 就可以将数组三等分。

 

示例 1：

输入：arr = [0,2,1,-6,6,-7,9,1,2,0,1]
输出：true
解释：0 + 2 + 1 = -6 + 6 - 7 + 9 + 1 = 2 + 0 + 1
示例 2：

输入：arr = [0,2,1,-6,6,7,9,-1,2,0,1]
输出：false
示例 3：

输入：arr = [3,3,6,5,-2,2,5,1,-9,4]
输出：true
解释：3 + 3 = 6 = 5 - 2 + 2 + 5 + 1 - 9 + 4
 

提示：

3 <= arr.length <= 5 * 104
-104 <= arr[i] <= 104
```

```

```

```
func canThreePartsEqualSum(arr []int) bool {
    sum := 0
    for _,value := range arr {
        sum += value
    }
    if sum % 3 != 0 {
        return false
    }
    find := sum / 3
    i := 0
    tmp := 0
    for i < len(arr) - 1 {
        tmp += arr[i]
        if tmp == find {
            break
        }
        i++
    }
    i++
    tmp1 := 0
    for i < len(arr) - 1 {
        tmp1 += arr[i]
        if tmp1 == find {
            break
        }
        i++
    }
    i++
    if i <= len(arr) - 1 {
        return true
    } else {
        return false
    }
}
```
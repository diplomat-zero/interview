```
输入整数数组 arr ，找出其中最小的 k 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

 

示例 1：

输入：arr = [3,2,1], k = 2
输出：[1,2] 或者 [2,1]
示例 2：

输入：arr = [0,1,2,1], k = 1
输出：[0]
 

限制：

0 <= k <= arr.length <= 10000
0 <= arr[i] <= 10000
```

```

```

```
func getLeastNumbers(arr []int, k int) []int {
    res := quickSort(arr, 0, len(arr) - 1, k)
    return res
}
func quickSort(arr []int, left int, right int, k int) []int {
    if left > right {
        return []int{}
    }
    num := findNum(arr, left, right)
    if num == k - 1 {
        return arr[:k]
    } 
    if num > k - 1 {
        return quickSort(arr, left, num - 1, k)
    }
    return quickSort(arr, num + 1, right, k)
}

func findNum(arr []int, left int, right int) int {
    target := arr[left]
    for left < right {
        for left < right && arr[right] >= target {
            right--
        }
        arr[left],arr[right] = arr[right],arr[left]
        for left < right && arr[left] <= target {
            left++
        }
        arr[left],arr[right] = arr[right],arr[left]
    }
    return left
}
```
```
编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

 

示例 1：

输入：strs = ["flower","flow","flight"]
输出："fl"
示例 2：

输入：strs = ["dog","racecar","car"]
输出：""
解释：输入不存在公共前缀。
 

提示：

1 <= strs.length <= 200
0 <= strs[i].length <= 200
strs[i] 仅由小写英文字母组成
```

```

```

```
func longestCommonPrefix(strs []string) string {
    if len(strs) == 0 {
        return ""
    }
    if len(strs) == 1 {
        return strs[0]
    }
    find := findlongest(strs[0], strs[1])
    if len(find) == 0 {
        return ""
    } 
    for i := 2; i < len(strs); i++ {
        find = findlongest(find, strs[i])
        if len(find) == 0 {
            return ""
        } 
    }
    return find
}

func findlongest(str1 string, str2 string) string {
    i := 0
	j := 0
	res := ""
	for i < len(str1) && j < len(str2) {
		char1 := string(str1[i])
		char2 := string(str2[j])
		if char1 != char2 {
			break
		}
		res += char1
		i++
		j++
	}
    return res
}
```
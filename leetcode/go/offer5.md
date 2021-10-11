```
请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

示例 1：
输入：s = "We are happy."
输出："We%20are%20happy."
 
限制
0 <= s 的长度 <= 10000
```

```
func replaceSpace(s string) string {
    ret := ""
	for _, ch := range s {
		apl := string(ch)
		if apl == " " {
			ret += "%20"
		} else {
			ret += apl
		}
	}

    return ret
}
```
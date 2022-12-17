```
输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，则输出"student. a am I"。

 

示例 1：

输入: "the sky is blue"
输出: "blue is sky the"
示例 2：

输入: "  hello world!  "
输出: "world! hello"
解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
示例 3：

输入: "a good   example"
输出: "example good a"
解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
 

说明：

无空格字符构成一个单词。
输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
```

```

```

```
func reverseWords(s string) string {
    s = strings.Trim(s, " ")
	stack := make([]string, 0)
	tmp := ""
	for i := 0; i < len(s); i++ {
		if string(s[i]) != " " {
			tmp = tmp + string(s[i])
		} else {
			if len(tmp) > 0 {
				stack = append(stack, tmp)
				tmp = ""
			}
		}
	}
	if len(tmp) != 0 {
		stack = append(stack, tmp)
	}
	res := ""
	for i := len(stack) - 1; i >= 0; i-- {
		res += stack[i]
		res += " "
	}
	return strings.Trim(res, " ")
}
```
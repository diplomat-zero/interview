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
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs.length == 0) {
            return "";
        }
        if (strs.length == 1) {
            return strs[0];
        }
        String find = findlongest(strs[0], strs[1]);
        for (int i = 2; i < strs.length; i++) {
            find = findlongest(find, strs[i]);
            if (find == "") {
                return find;
            }
        }
        return find;
    }

    public String findlongest(String str1, String str2) {
        StringBuilder s = new StringBuilder();
        int i = 0;
        int j = 0;
        while (i < str1.length() && j < str2.length()) {
            if (str1.charAt(i) != str2.charAt(j)) {
                break;
            }
            s.append(str1.charAt(i));
            i++;
            j++;
        }
        return s.toString();
    }
}
```
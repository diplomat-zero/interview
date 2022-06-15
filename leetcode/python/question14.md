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
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        def findPre(str1, str2):
            i = 0
            j = 0
            res = ''
            while i < len(str1) and j < len(str2):
                if str1[i] == str2[j]:
                    res = res + str1[i]
                    i += 1
                    j += 1
                else :
                    break
            
            return res
        if len(strs) == 0:
            return ''
        if len(strs) == 1:
            return strs[0]
        
        pre = findPre(strs[0], strs[1])
        if pre == '':
            return ''
        m = 2
        while m < len(strs):
            pre = findPre(strs[m], pre)
            if pre == '':
                return ''
            else :
                m += 1
        
        return pre
```
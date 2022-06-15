```
给定一个字符串 s ，找到 它的第一个不重复的字符，并返回它的索引 。如果不存在，则返回 -1 。

 

示例 1：

输入: s = "leetcode"
输出: 0
示例 2:

输入: s = "loveleetcode"
输出: 2
示例 3:

输入: s = "aabb"
输出: -1
 

提示:

1 <= s.length <= 105
s 只包含小写字母
```

```

```

```
class Solution:
    def firstUniqChar(self, s: str) -> int:
        map_dict = {}
        for i in range(len(s)):
            if s[i] in map_dict:
                map_dict[s[i]] = 'more'
            else:
                map_dict[s[i]] = i
        
        for m in map_dict:
            if map_dict[m] != 'more':
                return map_dict[m]
        
        return -1
```
```
字典 wordList 中从单词 beginWord 和 endWord 的 转换序列 是一个按下述规格形成的序列 beginWord -> s1 -> s2 -> ... -> sk：

每一对相邻的单词只差一个字母。
 对于 1 <= i <= k 时，每个 si 都在 wordList 中。注意， beginWord 不需要在 wordList 中。
sk == endWord
给你两个单词 beginWord 和 endWord 和一个字典 wordList ，返回 从 beginWord 到 endWord 的 最短转换序列 中的 单词数目 。如果不存在这样的转换序列，返回 0 。

 
示例 1：

输入：beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
输出：5
解释：一个最短转换序列是 "hit" -> "hot" -> "dot" -> "dog" -> "cog", 返回它的长度 5。
示例 2：

输入：beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
输出：0
解释：endWord "cog" 不在字典中，所以无法进行转换。
 

提示：

1 <= beginWord.length <= 10
endWord.length == beginWord.length
1 <= wordList.length <= 5000
wordList[i].length == beginWord.length
beginWord、endWord 和 wordList[i] 由小写英文字母组成
beginWord != endWord
wordList 中的所有字符串 互不相同
```

```

```

```
func ladderLength(beginWord string, endWord string, wordList []string) int {
    step := 1
    stack := make([]string, 0)
    stack = append(stack, beginWord)
    hash_map := make(map[string]bool)
    for _,value := range wordList {
        hash_map[value] = true
    }
    for len(stack) > 0 {
        length := len(stack)
        for i := 0; i < length; i++ {
            cur := stack[0]
            stack = stack[1:]
            if cur == endWord {
                return step
            }
            for c := 0; c < len(cur); c++ {
                for j := 'a'; j <= 'z'; j++ {
                    newWord := cur[:c] + string(j) + cur[c + 1:]
                    if hash_map[newWord] {
                        stack = append(stack, newWord)
                        hash_map[newWord] = false
                    }
                }
            }
        }
        step++
    }
    return 0
}
```
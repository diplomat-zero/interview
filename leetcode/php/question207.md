```
你这个学期必须选修 numCourses 门课程，记为 0 到 numCourses - 1 。

在选修某些课程之前需要一些先修课程。 先修课程按数组 prerequisites 给出，其中 prerequisites[i] = [ai, bi] ，表示如果要学习课程 ai 则 必须 先学习课程  bi 。

例如，先修课程对 [0, 1] 表示：想要学习课程 0 ，你需要先完成课程 1 。
请你判断是否可能完成所有课程的学习？如果可以，返回 true ；否则，返回 false 。

示例 1：
输入：numCourses = 2, prerequisites = [[1,0]]
输出：true
解释：总共有 2 门课程。学习课程 1 之前，你需要完成课程 0 。这是可能的。

示例 2：
输入：numCourses = 2, prerequisites = [[1,0],[0,1]]
输出：false
解释：总共有 2 门课程。学习课程 1 之前，你需要先完成​课程 0 ；并且学习课程 0 之前，你还应先完成课程 1 。这是不可能的。
 
提示：
1 <= numCourses <= 105
0 <= prerequisites.length <= 5000
prerequisites[i].length == 2
0 <= ai, bi < numCourses
prerequisites[i] 中的所有课程对 互不相同
```

```

```

```
class Solution {

    /**
     * @param Integer $numCourses
     * @param Integer[][] $prerequisites
     * @return Boolean
     */
    public $hascircle = false;
    public $visited = [];
    public $onPath = [];
    function canFinish($numCourses, $prerequisites) {
        $graph = $this->build($numCourses, $prerequisites);
        for ($i = 0; $i < $numCourses; $i++) {
            $this->dfs($graph, $i);
        }
        return !$this->hascircle;
    }

    function dfs($graph, $i) {
        if ($this->onPath[$i]) {
            $this->hascircle = true;
            return;
        }
        if ($this->visited[$i] || $this->hascircle) {
            return;
        }

        $this->visited[$i] = true;
        $this->onPath[$i] = true;
        foreach ($graph[$i] as $key => $value) {
            $this->dfs($graph, $value);
        }
        $this->onPath[$i] = false;
    }

    function build($numCourses, $prerequisites) {
        $graph = [];
        for ($i = 0; $i < $numCourses; $i++) {
            $graph[$i] = [];
        }
        foreach ($prerequisites as $value) {
            $to = $value[0];
            $from = $value[1];
            $graph[$from][] = $to;
        }
        return $graph;
    }
}
```
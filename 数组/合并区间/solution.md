```markdown
# 题目名称
合并数组

## 题目描述
[LeetCode 链接]([https://leetcode.com/problems/...](https://leetcode.cn/problems/merge-intervals/description/?envType=study-plan-v2&envId=top-100-liked))
以数组 intervals 表示若干个区间的集合，其中单个区间为 intervals[i] = [starti, endi] 。请你合并所有重叠的区间，并返回 一个不重叠的区间数组，该数组需恰好覆盖输入中的所有区间 。

示例 1：
输入：intervals = [[1,3],[2,6],[8,10],[15,18]]
输出：[[1,6],[8,10],[15,18]]
解释：区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].

示例 2：
输入：intervals = [[1,4],[4,5]]
输出：[[1,5]]
解释：区间 [1,4] 和 [4,5] 可被视为重叠区间。

示例 3：
输入：intervals = [[4,7],[1,4]]
输出：[[1,7]]
解释：区间 [1,4] 和 [4,7] 可被视为重叠区间。
 
提示：
1 <= intervals.length <= 104
intervals[i].length == 2
0 <= starti <= endi <= 104

## 解法一：排序+遍历
```javascript
var merge = function(intervals) {
    //边界处理
    if (intervals.length === 1){
        return intervals;
    }

    intervals.sort((a,b) => a[0] - b[0]);   //箭头函数
    const result = [];

    let i = 0;
    while (i < intervals.length){
        //通过看变量声明，可以清楚知道start是只读，end会被修改
        const start = intervals[i][0];   
        let end = intervals[i][1];

        let j = i + 1;
        while (j < intervals.length && intervals[j][0] <= end) { //不能忘记j的约束条件
            end = Math.max(end, intervals[j][1]);
            j++;
        }

        result.push([start, end]);
        i = j;
    }
    return result;
};
```
```markdown
## 思路：
1.先排序，后面才方便比较。
2.按顺序遍历一个个区间，检查与下一个区间是否重叠，如有重叠，就合并区间，
  直到找出这个不连续的独立区间，把这个区间加入result，再接着检查下一个区间。

## 思考：
1.while和for的区别
  疑问：这里为什么要用while，而不用for？明明会遍历每一个区间，循环次数是确定的。
  答：首先，循环次数并不是确定的，虽然整体来说会遍历每一个区间，但分为外层循环和内层循环，
      也就是说，外层循环次数加上内层循环次数是确定的，但他们分别循环次数是不确定的，因此不能用for，而用while。
      简单来理解，while是跳跃式前进，比如i = j；for是顺序遍历，比如i++。
      除此之外，在写法上，while的循环变量在外部定义，for的循环变量在内部定义。

## 应用
1.日程管理：合并细碎工作时间，算出忙碌区间；
2.项目时间线/甘特图：合并多个任务的时间区间，得到总项目长；
也就是说，不受重叠区间影响，依然可以算出总和


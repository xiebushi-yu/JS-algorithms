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
```
var merge = function(intervals) {
    if (intervals.length === 1){
        return intervals;
    }
    intervals.sort((a,b) => a[0] - b[0]);
    const result = [];
    let i = 0;
    while (i < intervals.length){
        const start = intervals[i][0];   
        let end = intervals[i][1];  
        let j = i + 1;
        while (j < intervals.length && intervals[j][0] <= end) {
            end = Math.max(end, intervals[j][1]);
            j++;
        }
        result.push([start, end]);
        i = j;
    }
    return result;
};
```

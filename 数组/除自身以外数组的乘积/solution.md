
# 题目名称
合并数组

## 题目描述
https://leetcode.cn/problems/product-of-array-except-self/description/?envType=study-plan-v2&envId=top-100-liked  

给你一个整数数组 nums，返回 数组 answer ，其中 answer[i] 等于 nums 中除了 nums[i] 之外其余各元素的乘积 。  
题目数据 保证 数组 nums之中任意元素的全部前缀元素和后缀的乘积都在  32 位 整数范围内。  
请 不要使用除法，且在 O(n) 时间复杂度内完成此题。

示例 1:  
输入: nums = [1,2,3,4]  
输出: [24,12,8,6]  

示例 2:  
输入: nums = [-1,1,0,-3,3]  
输出: [0,0,9,0,0]  
 
提示：  
2 <= nums.length <= 105  
-30 <= nums[i] <= 30  
输入 保证 数组 answer[i] 在  32 位 整数范围内  

## 解法一：前缀积*后缀积
```javascript
var productExceptSelf = function(nums) {
    const n = nums.length;
    const left = new Array(n);
    const right = new Array(n);
    const answer = new Array(n);

    left[0] = 1;
    for (let i = 1; i < n; i++){     //0号位已经有了，于是从1号位开始
        left[i] = left[i - 1] * nums[i - 1];
    }

    right[n - 1] = 1;
    for (let i = n-2; i >= 0; i--){
        right[i] = right[i + 1] * nums[i + 1];
    }

    for (let i = 0; i < n; i++){
        answer[i] = left[i] * right[i];
    }
    return answer;
};
```

### 思路：
1. 分别计算前缀积和后缀积。  
2. 将两数组相乘得到结果数组。

### 思考：
 **如何理解"前缀""前缀"**  
 
  **疑问：**
  这里为什么要用while，而不用for？明明会遍历每一个区间，循环次数是确定的。
  
  **答：**
  *首先*，循环次数并不是确定的，虽然整体来说会遍历每一个区间，但分为外层循环和内层循环，也就是说，外层循环次数加上内层循环次数是确定的，但他们分别循环次数是不确定的，因此不能用for，而用while。*简单来理解*，while是跳跃式前进，比如i = j；for是顺序遍历，比如i++。 *除此之外*，在写法上，while的循环变量在外部定义，for的循环变量在内部定义。

## 应用
- 日程管理：合并细碎工作时间，算出忙碌区间；
- 项目时间线/甘特图：合并多个任务的时间区间，得到总项目长；  
也就是说，不受重叠区间影响，依然可以算出总和

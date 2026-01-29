
# 题目名称
轮转数组

## 题目描述
https://leetcode.cn/problems/rotate-array/description/?envType=study-plan-v2&envId=top-100-liked  

给定一个整数数组 nums，将数组中的元素向右轮转 k 个位置，其中 k 是非负数。

示例 1:
输入: nums = [1,2,3,4,5,6,7], k = 3  
输出: [5,6,7,1,2,3,4]  
解释:
向右轮转 1 步: [7,1,2,3,4,5,6]
向右轮转 2 步: [6,7,1,2,3,4,5]
向右轮转 3 步: [5,6,7,1,2,3,4]  

示例 2:
输入：nums = [-1,-100,3,99], k = 2  
输出：[3,99,-1,-100]  
解释: 
向右轮转 1 步: [99,-1,-100,3]
向右轮转 2 步: [3,99,-1,-100]
 
提示：
1 <= nums.length <= 105
-231 <= nums[i] <= 231 - 1
0 <= k <= 105

## 解法一：环状替换
```javascript
var rotate = function(nums, k) {
    //处理k比数组长度大的情况
    const n = nums.length;
    k = k % n;
    //有几个数完成位置转移
    let count = 0;
    for (let start = 0; count < n; start++){
        let curr = start;                           //数组第几个位置正在进行转移（A的位置）（即操作位置）
        let prev = nums[start];                     //正要转移的那个数A
        do{
            const next = (curr + k) % n;            //A要去的位置
            const temp = nums[next];                //让A要去位置上的数站起来（保存住这个数）
            nums[next] = prev;                      //A坐上了目标位置
            prev = temp;                            //现在轮到下一个数转移
            curr = next;                            //操作位置来到了下一个
            count++;                                //完成一个数就加一
        }while (start !== curr);  
    }
};
```

### 思路：
1. 把每个元素直接放到它的最终位置。  
2. 一次处理一个环。
3. 注意k可能大于n。

### 思考：
 **如何理解环状替代**  

  **答：**
  借助抢凳子游戏理解，关键在于一人一个位置。  
  首先确定操作的元素，让它站起来，定为prev，那么它原本所在的位置，即为curr，算出它的最终位置，即为next，让最终位置上的元素站起来，即temp，接着让它坐上自己最终的位置，prev坐上了next。然后准备开启下一轮，将站起来的元素定为prev，再将它原本的位置定为curr。

## 应用
- 音乐循环播放；
- 环形缓存区；

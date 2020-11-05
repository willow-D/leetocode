# 题目

leetcode : [打家劫舍](https://leetcode-cn.com/problems/house-robber/)

## dp
```Java
class Solution {
    public int rob(int[] nums) {
        if(nums.length==0){
            return 0;
        }
        int[] dp = new int[nums.length+1];
        dp[1] = nums[0];
        for(int i=1;i<nums.length;i++){
            dp[i+1] = Math.max(dp[i], dp[i-1]+nums[i]);
        }
        return dp[nums.length];
    }
}
```

## 状态压缩
```Java
class Solution {
    public int rob(int[] nums) {
        if(nums.length==0){
            return 0;
        }
        int i_2 = 0;
        int i_1 = nums[0];
        for(int i=1;i<nums.length;i++){
            int tem = Math.max(i_1, i_2+nums[i]);
            i_2 = i_1;
            i_1 = tem;
        }
        return i_1;
    }
}
```

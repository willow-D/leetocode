# 题目

leetcode : [最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)

## dp
```Java
class Solution {
    public int maxSubArray(int[] nums) {
        int res = Integer.MIN_VALUE;
        int pre = 0;
        for(int n : nums){
            if(pre>=0){
                pre+=n;
            }
            else{
                pre = n;
            }
            res = Math.max(res, pre);
        }
        return res;
    }
}
```

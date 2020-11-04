# 题目
leetcode : [乘积最大子数组](https://leetcode-cn.com/problems/maximum-product-subarray/)

## dp
```Java
class Solution {
    public int maxProduct(int[] nums) {
        int max_ = nums[0];
        int min_ = nums[0];
        int res = nums[0];
        for(int i=1;i<nums.length;i++){
            int temMax = max_;
            int temMin = min_;
            if(nums[i]>0){
                max_ = Math.max(nums[i]*temMax, nums[i]);
                min_ = Math.min(nums[i]*temMin, nums[i]);
            }
            else{
                max_ = Math.max(nums[i]*temMin, nums[i]);
                min_ = Math.min(nums[i]*temMax, nums[i]);
            }
            res = Math.max(res, max_);
        }
        return res;
    }
}
```

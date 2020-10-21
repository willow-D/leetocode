# 题目

leetcode : [下一个排列](https://leetcode-cn.com/problems/next-permutation/submissions/)

## 字典序
```Java
class Solution {
    public void nextPermutation(int[] nums) {
        if(nums==null || nums.length==0){
            return;
        }
        for(int i=nums.length-1;i>0;i--){
            if(nums[i-1]>=nums[i]){
                continue;
            }
            for(int j=nums.length-1;j>=i;j--){
                if(nums[j]>nums[i-1]){
                    swap(nums, i-1, j);
                    reverse(nums, i);
                    return;
                }
            }
        }
        reverse(nums, 0);
        return;
    }
    public void swap(int[] nums, int i, int j){
        int tem = nums[i];
        nums[i] = nums[j];
        nums[j] = tem;
    }
    
    public void reverse(int[] nums, int start){
        int i=start;
        int j = nums.length-1;
        while(i<j){
            swap(nums, i, j);
            i++;
            j--;
        }
    }
}
```

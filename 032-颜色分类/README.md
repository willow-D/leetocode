# 题目
leetcode : [颜色分类](https://leetcode-cn.com/problems/sort-colors/submissions/)

## 荷兰旗问题
```Java
class Solution {
    public void sortColors(int[] nums) {

        int left = -1;
        int right = nums.length;
        int index = 0;
        while(index<right){
            if(nums[index]<1){
                swap(nums, left+1, index);
                left++;
                index++;
            }
            else if(nums[index]==1){
                index++;
            }
            else{
                swap(nums, right-1, index);
                right--;
            }
        }
        return ; 
    }

    public void swap(int[] nums, int i, int j){
        int tem = nums[i];
        nums[i] = nums[j];
        nums[j] = tem;
    }
}
```

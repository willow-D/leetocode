# 题目

leetcode : [在排序数组中查找元素的第一个和最后一个位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

## 二分
```Java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int f = first(nums, target);
        int l = last(nums, target);
        return new int[]{f,l};

    }

    public int first(int[] nums, int target){
        int res = -1;
        int left = 0;
        int right = nums.length - 1;

        while(left<=right){
            int mid = left + (right - left)/2;
            if(nums[mid]>target){
                right = mid - 1;
            }
            else if(nums[mid]<target){
                left = mid + 1;
            }
            else{
                res = mid;
                right = mid - 1;
            }
        }
        return res;
    }

    public int last(int[] nums, int target){
        int res = -1;
        int left = 0;
        int right = nums.length - 1;

        while(left<=right){
            int mid = left + (right - left)/2;
            if(nums[mid]>target){
                right = mid - 1;
            }
            else if(nums[mid]<target){
                left = mid + 1;
            }
            else{
                res = mid;
                left = mid + 1;
            }
        }
        return res;
    }
}
```

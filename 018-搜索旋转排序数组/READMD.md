# 题目
leetcode : [搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/submissions/)

## 二分查找
- 查找分割点，转化为两段有序的子数组，然后分别二分查找
```Java
class Solution {
    public int search(int[] nums, int target) {
        int point = findPoint(nums);
        if(-1==binarySearch(nums, target, 0, point-1)){
            return binarySearch(nums, target, point, nums.length-1);
        }
        return binarySearch(nums, target, 0, point-1);
    }

    public int findPoint(int[] nums){
        int left = 0;
        int right = nums.length - 1;
        if(nums[right]>=nums[left]){
            return right+1;
        }
        int mid = 0;
        while(left<=right){
            mid = left + (right - left)/2;
            if(nums[mid]>=nums[0]){
                left = mid + 1;
                continue;
            }
            if(nums[mid]>nums[mid-1]){
                right = mid - 1;
            }
            else{
                break;
            }
        }
        return  mid;

    }
    public int binarySearch(int[] nums, int target, int start, int end){
        while(start<=end){
            int mid = start + (end - start)/2;
            if(nums[mid]>target){
                end = mid - 1;
            }
            else if(nums[mid]<target){
                start = mid + 1;
            }
            else{
                return mid;
            }
        }
        return -1;
    }
}

```

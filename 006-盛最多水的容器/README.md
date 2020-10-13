# 题目
leetcode : [盛最多水的容器](https://leetcode-cn.com/problems/container-with-most-water/submissions/)

## 双指针维护一个动态区间
```Java
class Solution {
    public int maxArea(int[] height) {
        int left = 0;
        int right = height.length-1;

        int area = 0;
        while(left<right){
            int tem = (right-left)*Math.min(height[left], height[right]);
            area = Math.max(area, tem);
            if(height[left]<=height[right]){
                left+=1;
            }
            else{
                right-=1;
            }
        }
        return area;
    }
}
```

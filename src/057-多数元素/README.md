# 题目

leetcode : [多数元素](https://leetcode-cn.com/problems/majority-element/)

## 柱形图理解
```Java
class Solution {
    public int majorityElement(int[] nums) {
        int curNum = nums[0];
        int cnt = 0;
        for(int i=0;i<nums.length;i++){
            if(nums[i]==curNum){
                cnt++;
            }
            else if(cnt==0){
                curNum = nums[i];
                cnt++;
            }
            else{
                cnt--;
            }
        }
        return curNum;
    }
}
```

# 题目

leetcode ： [跳跃游戏](https://leetcode-cn.com/problems/jump-game/)

```Java
class Solution {
    public boolean canJump(int[] nums) {
        int maxRight = 0;
        int index = 0;
        while(index<nums.length && index<=maxRight){
            maxRight = Math.max(maxRight, index+nums[index]);
            index++;
        }
        return maxRight>=nums.length-1 ? true : false;
    }
}
```

# 题目
leetcode : [最长连续序列](https://leetcode-cn.com/problems/longest-consecutive-sequence/)

## 空间换时间 遍历技巧
```Java
class Solution {
    public int longestConsecutive(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for(int n:nums){
            set.add(n);
        }
        int res = 0;
        for(int n:nums){
            if(!set.contains(n-1)){
                int curNum = n;
                int curLong = 1;

                while(set.contains(curNum+1)){
                    curNum++;
                    curLong++;
                }
                res = Math.max(res, curLong);
            }
        }
        return res;
    }
}
```

# 题目

leetcode : [求众数II](https://leetcode-cn.com/problems/majority-element-ii/)

## 柱形图理解
```Java
class Solution {
    public List<Integer> majorityElement(int[] nums) {
        List<Integer> res = new LinkedList<>();
        if(nums.length==0){
            return res;
        }
        int A = nums[0];
        int B = nums[0];
        int cntA = 0;
        int cntB = 0;
        for(int n:nums){
            if(n==A){
                cntA++;
            }
            else if(n==B){
                cntB++;
            }
            else if(cntA==0){
                A = n;
                cntA++;
            }
            else if(cntB==0){
                B = n;
                cntB++;
            }
            else{
                cntA--;
                cntB--;
            }
        }
        cntA = 0;
        cntB = 0;
        for(int n:nums){
            if(n==A){
                cntA++;
            }
            else if(n==B){
                cntB++;
            }
        }
        if(cntA>nums.length/3){
            res.add(A);
        }
        if(cntB>nums.length/3){
            res.add(B);
        }
        return res;
    }
}
```

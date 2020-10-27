# 题目

leetcode : [不同的二叉搜索树](https://leetcode-cn.com/problems/unique-binary-search-trees/)

## dp
```Java
class Solution {
    public int numTrees(int n) {
        if(n<2){
            return n;
        }
        int[] dp = new int[n+1];
        dp[0] = 1;
        dp[1] = 1;
        for(int i=2;i<=n;i++){
            for(int j=0;j<i;j++){
                dp[i]+= (dp[j]*dp[i-1-j]);
            }
        }
        return dp[n];
    }
}
```

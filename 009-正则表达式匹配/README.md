# 题目

leetcode ：[正则表达式匹配](https://leetcode-cn.com/problems/regular-expression-matching/)

## 动态规划
- s==null  p!=null 的情况需要特判
```Java

class Solution {
    public boolean isMatch(String s, String p) {
        if(p.length()!=0 && p.charAt(0)=='*'){
            return false;
        }
        boolean[][] dp = new boolean[p.length()+1][s.length()+1];
        dp[0][0] = true;
        for(int i=0;i<p.length();i++){
            if(p.charAt(i)=='*'){
                dp[i+1][0] = dp[i-1][0];
            }
        }

        for(int i=0;i<p.length();i++){
            for(int j=0;j<s.length();j++){
                if(p.charAt(i)>='a'&&p.charAt(i)<='z'){
                    if(p.charAt(i)==s.charAt(j)){
                        dp[i+1][j+1] = dp[i][j];
                    }
                    else{
                        dp[i+1][j+1] = false;
                    }
                }
                else if(p.charAt(i)=='.'){
                    dp[i+1][j+1] = dp[i][j];
                }
                else{
                    if(p.charAt(i-1)=='.' || p.charAt(i-1)==s.charAt(j)){
                        dp[i+1][j+1] = dp[i+1][j] || dp[i-1][j+1];
                    }
                    else{
                        dp[i+1][j+1] = dp[i-1][j+1];
                    }
                }
            }
        }
        return dp[p.length()][s.length()];
    }
}
```

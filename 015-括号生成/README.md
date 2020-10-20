# 题目
leetcode : [括号生成](https://leetcode-cn.com/problems/generate-parentheses/)

## dfs + 回溯 （优化后）
```Java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> ans = new ArrayList<String>();
        backtrack(ans, new StringBuilder(), 0, 0, n);
        return ans;
    }

    public void backtrack(List<String> ans, StringBuilder cur, int open, int close, int max) {
        if (cur.length() == max * 2) {
            ans.add(cur.toString());
            return;
        }
        if (open < max) {
            cur.append('(');
            backtrack(ans, cur, open + 1, close, max);
            cur.deleteCharAt(cur.length() - 1);
        }
        if (close < open) {
            cur.append(')');
            backtrack(ans, cur, open, close + 1, max);
            cur.deleteCharAt(cur.length() - 1);
        }
    }
}


```


## 优化前
```Java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> res = new LinkedList<>();
        StringBuilder parenthesis = new StringBuilder();
        parenthesis.append('(');
        dfs(res, n-1, n, parenthesis);
        return res;
    }

    public void dfs(List<String> res, int leftNum, int rightNum, StringBuilder parenthesis){
    if((leftNum+rightNum)==0){
        res.add(parenthesis.toString());
        return;
    }
    Character c = parenthesis.charAt(parenthesis.length()-1);
    if(leftNum==0){
        parenthesis.append(')');
        dfs(res, leftNum, rightNum-1, parenthesis);
        parenthesis.deleteCharAt(parenthesis.length()-1);
        return;
    }
    if(rightNum==0){
        parenthesis.append('(');
        dfs(res, leftNum-1, rightNum, parenthesis);
        parenthesis.deleteCharAt(parenthesis.length()-1);
        return;                
    }

    parenthesis.append('(');
    dfs(res, leftNum-1, rightNum, parenthesis);
    parenthesis.deleteCharAt(parenthesis.length()-1);

    if(leftNum<rightNum){
        parenthesis.append(')');
        dfs(res, leftNum, rightNum-1, parenthesis);
        parenthesis.deleteCharAt(parenthesis.length()-1);
    }
}


}
```

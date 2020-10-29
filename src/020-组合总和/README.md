# 题目

leetcode : [组合总和](https://leetcode-cn.com/problems/combination-sum/)

## dfs + 回溯
- 先对数组进行排序，避免重复的组合
```Java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        Arrays.sort(candidates);
        List<List<Integer>> res = new LinkedList<List<Integer>>();
        LinkedList<Integer> combination = new LinkedList<>();
        dfs(res, candidates, 0, target, combination);
        return res;
    }
    public void dfs(List<List<Integer>> res, int[] candidates, int start, int target, LinkedList<Integer> combination){
        if(target<0){
            return;
        }
        if(target==0){
            res.add(new LinkedList<Integer>(combination));
            return;
        }
        for(int i=start;i<candidates.length;i++){
            combination.add(candidates[i]);
            dfs(res, candidates, i, target-candidates[i], combination);
            combination.removeLast();
        }
    }
}
```

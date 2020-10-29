# 题目

leetcode : [全排列](https://leetcode-cn.com/problems/permutations/)

## dfs + 回溯

```Java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new LinkedList<List<Integer>>();
        LinkedList<Integer> per = new LinkedList<>();
        int[] used = new int[nums.length];
        dfs(res, nums, used, per);
        return res;
    }

    public void dfs(List<List<Integer>> res, int[] nums, int[] used, LinkedList<Integer> per){
        if(per.size()==nums.length){
            res.add(new LinkedList<Integer>(per));
            return;
        }
        for(int i=0;i<nums.length;i++){
            if(used[i]==0){
                per.add(nums[i]);
                used[i] = 1;
                dfs(res, nums, used, per);
                per.removeLast();
                used[i] = 0;
            }
        }
    }
}
```

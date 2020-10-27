# 题目

leetcode : [子集](https://leetcode-cn.com/problems/subsets/)

## dfs + 回溯
```Java
class Solution {
        public List<List<Integer>> subsets(int[] nums) {
            List<List<Integer>> res = new LinkedList<List<Integer>>();
            LinkedList<Integer> set = new LinkedList<>();
            dfs(res, 0, nums, set);
            return res;
        }
        
        public void dfs(List<List<Integer>> res, int start, int[] nums, LinkedList<Integer> set){
            res.add(new LinkedList<Integer>(set));
            for(int i=start;i<nums.length;i++){
                set.add(nums[i]);
                dfs(res, i+1, nums, set);
                set.removeLast();
            }
        }
}
```

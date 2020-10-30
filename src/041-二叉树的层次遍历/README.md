# 题目
leetcode : [二叉树的层次遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

## 队列
```Java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new LinkedList<List<Integer>>();
        if(root==null){
            return res;
        }
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        
        while(!queue.isEmpty()){
            List<Integer> level = new LinkedList<>();
            int cnt = queue.size();
            while(cnt>0){
                root = queue.poll();
                level.add(root.val);
                if(root.left!=null){
                    queue.add(root.left);
                }
                if(root.right!=null){
                    queue.add(root.right);
                }
                cnt--;
            }
            res.add(level);
        }
        return res;
    }
}
```

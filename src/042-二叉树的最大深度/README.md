#题目

leetcode : [二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)

## 递归
```Java
class Solution {
    public int maxDepth(TreeNode root) {
        if(root==null){
            return 0;
        }
        if(root.left==null && root.right==null){
            return 1;
        }
        return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));

    }
}
```

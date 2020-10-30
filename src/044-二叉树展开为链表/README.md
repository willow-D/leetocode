# 题目

leetcode : [二叉树展开为链表](https://leetcode-cn.com/problems/flatten-binary-tree-to-linked-list/)

## 递归
```Java
class Solution {
    public void flatten(TreeNode root) {
        if(root==null){
            return;
        }
        TreeNode left = root.left;
        TreeNode right = root.right;
        flatten(left);
        flatten(right);

        root.left = null;
        root.right = left;
        TreeNode end = root;
        while(end.right!=null){
            end = end.right;
        }
        end.right = right;
        return ;
    }
}
```

# 题目

leetcode : [从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

## 递归
```Java
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        return buildTree(preorder, 0, inorder, 0, inorder.length-1);

    }
    public TreeNode buildTree(int[] preorder, int i, int[] inorder, int start, int end){
        TreeNode root = null;
        if(start>end){
            return root;
        }
        for(int j=start;j<=end;j++){
            if(inorder[j]==preorder[i]){
                root = new TreeNode(preorder[i]);
                root.left = buildTree(preorder, i+1, inorder, start, j-1);
                root.right = buildTree(preorder, i+1+j-start, inorder, j+1, end);  // ?
                break;
            }
        }
        return root;
    }
}
```

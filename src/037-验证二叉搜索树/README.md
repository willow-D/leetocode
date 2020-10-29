# 题目

leetcode : [验证二叉搜索树](https://leetcode-cn.com/problems/validate-binary-search-tree/)


## 递归判断
```Java
class Solution {
    public boolean isValidBST(TreeNode root) {
        if(root==null){
            return true;
        }
        TreeNode rightNode = root.right;
        TreeNode leftNode = root.left;
        while(rightNode!=null && rightNode.left!=null){
            rightNode = rightNode.left;
        }
        if(rightNode!=null && rightNode.val<=root.val){
            return false;
        }
        while(leftNode!=null && leftNode.right!=null){
            leftNode = leftNode.right;
        }
        if(leftNode!=null && leftNode.val>=root.val){
            return false;
        }
        
        return isValidBST(root.left) && isValidBST(root.right);
    }
}
```

## 二叉搜索树中序遍历之后是递增序列
```Java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isValidBST(TreeNode root) {
        List<Integer> arr = mid(root);

        for(int i=0;i<arr.size()-1;i++){
            if(arr.get(i)>=arr.get(i+1)){
                return false;
            }
        }
        return true;
    }

    public List<Integer> mid(TreeNode root){
        List<Integer> res = new LinkedList<>();
        Stack<TreeNode> stack = new Stack<>();
        while(!stack.empty() || root!=null){
            if(root!=null){
                stack.add(root);
                root = root.left;
            }
            else{
                root = stack.pop();
                res.add(root.val);
                root = root.right;
            }
        }
        return res;
    }
}


```

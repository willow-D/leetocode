# 题目

leetcode : [二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/submissions/)

## 递归
```Java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new LinkedList<>();
        mid(root, res);     
        return res;
    }

    public void mid(TreeNode root, List<Integer> res){
        if(root==null){
            return;
        }
        mid(root.left, res);
        res.add(root.val);
        mid(root.right, res);
    }
}

```

## 迭代
```Java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {

        List<Integer> res = new LinkedList<>();
        if(root==null){
            return res;
        }
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

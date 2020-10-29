# 题目

leetcode : [对称二叉树](https://leetcode-cn.com/problems/symmetric-tree/)

## 递归
```Java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return isSymmetric(root, root);
    }

    public boolean isSymmetric(TreeNode root1, TreeNode root2){
        if(root1==null && root2==null){
            return true;
        }
        if(root1==null || root2==null){
            return false;
        }
        if(root1.val != root2.val){
            return false;
        }
        return isSymmetric(root1.left, root2.right) && isSymmetric(root1.right, root2.left);
    }
}
```

## 迭代
```Java

class Solution {
    public boolean isSymmetric(TreeNode root) {
        return isSymmetric(root, root);
        
    }

    public boolean isSymmetric(TreeNode root1, TreeNode root2){
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root1);
        queue.add(root2);

        while(!queue.isEmpty()){
            root1 = queue.poll();
            root2 = queue.poll();
            if(root1==null && root2==null){
                continue;
            }
            if(root1==null || root2==null){
                return false;
            }
            if(root1.val!=root2.val){
                return false;
            }
            queue.add(root1.left);
            queue.add(root2.right);
            queue.add(root1.right);
            queue.add(root2.left);
        }
        return true;
    }

}
```

### 中序遍历判断回文字符串是不可以的，中序遍历不足于确定一棵树

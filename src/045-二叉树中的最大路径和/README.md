# 题目

leetcode : [二叉树中的最大路径和](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/)

## 递归
```Java
class Solution {
    int maxSum = Integer.MIN_VALUE;

    public int maxPathSum(TreeNode root) {
        maxGain(root);
        return maxSum;
    }

    public int maxGain(TreeNode node) {
        if (node == null) {
            return 0;
        }
        
        // 递归计算左右子节点的最大贡献值
        // 只有在最大贡献值大于 0 时，才会选取对应子节点
        int leftGain = Math.max(maxGain(node.left), 0);
        int rightGain = Math.max(maxGain(node.right), 0);

        // 节点的最大路径和取决于该节点的值与该节点的左右子节点的最大贡献值
        int priceNewpath = node.val + leftGain + rightGain;

        // 更新答案
        maxSum = Math.max(maxSum, priceNewpath);

        // 返回节点的最大贡献值
        return node.val + Math.max(leftGain, rightGain);
    }
}
```

## 用栈改为迭代，map记忆化，避免大量重复计算
```Java
class Solution {
    public int maxPathSum(TreeNode root) {
        if(root==null){
            return 0;
        }
        Map<TreeNode, Integer> map = new HashMap<>();
        int res = Integer.MIN_VALUE;
        Stack<TreeNode> stack = new Stack<>();
        while(!stack.empty() || root!=null){
            if(root!=null){
                res = Math.max(res, root.val+pathSum(root.left, map)+pathSum(root.right, map));             
                stack.add(root);
                root = root.left;
            }
            else{
                root = stack.pop();
                root = root.right;
            }
        }
        return res;
    }

    public int pathSum(TreeNode root, Map<TreeNode, Integer> map){
        if(root==null){
            return 0;
        }
        if(map.containsKey(root)){
            return map.get(root);
        }

        int res = root.val;
        int tem = Math.max(pathSum(root.right, map), pathSum(root.left, map));
        tem = Math.max(0, tem);
        res+=tem;
        res = Math.max(res, 0);
        map.put(root, res);

        return res;
    }
}
```

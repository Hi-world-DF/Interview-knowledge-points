# Tree
* [1.ContainsDuplicate（判断是否存在重复元素）]()
* [2.MergeTwoBinaryTrees（合并二叉树）]()
* [3.InvertBinaryTree（翻转二叉树）]()
* [4.BalancedBinaryTree（平衡二叉树判断）]()
* [5.DiameterOfBinaryTree（二叉树的直径）]()
* [6.PathSum（路径总和）]()

## 1.MaximumDepthOfBinaryTree（二叉树的最大深度）
问题描述：[LeetCode](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)   
代码：
``` java 
/**
 * 数据结构：树【递归】
 * leetcode:https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/
 * 题目描述：二叉树的最大深度
 * */

public class MaximumDepthOfBinaryTree {
    public int maxDepth(TreeNode root) {
        if(root == null){
            return 0;
        }
        int l = maxDepth(root.left);
        int r = maxDepth(root.right);
        return Math.max(l,r)+1;
    }
}
```
## 2.MergeTwoBinaryTrees（合并二叉树）
问题描述：[LeetCode](https://leetcode-cn.com/problems/merge-two-binary-trees/)   
代码：
``` java 
/**
 * 数据结构：树【递归】
 * leetcode:https://leetcode-cn.com/problems/merge-two-binary-trees/
 * 题目描述：合并二叉树
 * */
public class MergeTwoBinaryTrees {
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if(t1 == null && t2== null) return null;
        if(t1 == null) return t2;
        if(t2 == null) return t1;
        TreeNode root = new TreeNode(t1.val+t2.val);
        root.val = t1.val + t2.val;
        root.left = mergeTrees(t1.left,t2.left);
        root.right = mergeTrees(t1.right,t2.right);
        return root;
    }
}
```
## 3.InvertBinaryTree（翻转二叉树）
问题描述：[LeetCode](https://leetcode-cn.com/problems/invert-binary-tree/)   
代码：
``` java 
/**
 * 数据结构：树【递归】
 * leetcode:https://leetcode-cn.com/problems/invert-binary-tree/
 * 题目描述：翻转二叉树
 * */
public class InvertBinaryTree {
    public TreeNode invertTree(TreeNode root) {
        if(root == null){
            return null;
        }
        //先保存右子树的指针，然后让root右指针指向左子树，左指针指向右子树指针
        TreeNode right = root.right;
        root.right = invertTree(root.left);
        root.left = invertTree(right);
        return root;
    }
}
```
## 4.BalancedBinaryTree（平衡二叉树判断）
问题描述：[LeetCode](https://leetcode-cn.com/problems/balanced-binary-tree/)   
代码：
``` java 
/**
 * 数据结构：树【递归】
 * leetcode:https://leetcode-cn.com/problems/balanced-binary-tree/
 * 题目描述：平衡二叉树判断
 * */
public class BalancedBinaryTree {
    private boolean result = true;
    public boolean isBalanced(TreeNode root) {
        maxDepth(root);
        return result;
    }
    private int maxDepth(TreeNode root) {
        if(root == null){
            return 0;
        }
        int l = maxDepth(root.left);
        int r = maxDepth(root.right);
        if(Math.abs(l-r)> 1){
            result = false;
        }
        return 1 + Math.max(l,r);
    }
}
```
## 5.DiameterOfBinaryTree（二叉树的直径）
问题描述：[LeetCode](https://leetcode-cn.com/problems/diameter-of-binary-tree/)   
代码：
``` java 
/**
 * 数据结构：树【递归】
 * leetcode:https://leetcode-cn.com/problems/diameter-of-binary-tree/
 * 题目描述：二叉树的直径
 * */
public class DiameterOfBinaryTree {
    private int result = 0;
    public int diameterOfBinaryTree(TreeNode root) {
        maxDepth(root);
        return result;
    }

    private int maxDepth(TreeNode root) {
        if(root == null){
            return 0;
        }
        int l = maxDepth(root.left);
        int r = maxDepth(root.right);
        result = Math.max(result,l+r);
        return Math.max(l,r)+1;
    }
}
```
## 6.PathSum（路径总和）
问题描述：[LeetCode](https://leetcode-cn.com/problems/path-sum/)   
代码：
``` java 
/**
 * 数据结构：树【递归】
 * leetcode:https://leetcode-cn.com/problems/path-sum/
 * 题目描述：路径总和
 * */
public class PathSum {
    public boolean hasPathSum(TreeNode root, int sum) {
        if(root == null){
            return false;
        }
        if(root.right == null && root.left == null && root.val == sum){
            return true;
        }
        if(hasPathSum(root.left,sum-root.val)  || hasPathSum(root.right,sum-root.val)){
            return true;
        }
        return false;
    }
}
```

# Tree
* [1.ContainsDuplicate（判断是否存在重复元素）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/Tree.md#1maximumdepthofbinarytree%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E5%A4%A7%E6%B7%B1%E5%BA%A6)
* [2.MergeTwoBinaryTrees（合并二叉树）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/Tree.md#2mergetwobinarytrees%E5%90%88%E5%B9%B6%E4%BA%8C%E5%8F%89%E6%A0%91)
* [3.InvertBinaryTree（翻转二叉树）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/Tree.md#3invertbinarytree%E7%BF%BB%E8%BD%AC%E4%BA%8C%E5%8F%89%E6%A0%91)
* [4.BalancedBinaryTree（平衡二叉树判断）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/Tree.md#4balancedbinarytree%E5%B9%B3%E8%A1%A1%E4%BA%8C%E5%8F%89%E6%A0%91%E5%88%A4%E6%96%AD)
* [5.DiameterOfBinaryTree（二叉树的直径）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/Tree.md#5diameterofbinarytree%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E7%9B%B4%E5%BE%84)
* [6.PathSum（路径总和）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/Tree.md#6pathsum%E8%B7%AF%E5%BE%84%E6%80%BB%E5%92%8C)

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

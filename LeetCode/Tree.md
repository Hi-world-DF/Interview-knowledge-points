# Tree
* [1.ContainsDuplicate（判断是否存在重复元素）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/Tree.md#1maximumdepthofbinarytree%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E5%A4%A7%E6%B7%B1%E5%BA%A6)
* [2.MergeTwoBinaryTrees（合并二叉树）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/Tree.md#2mergetwobinarytrees%E5%90%88%E5%B9%B6%E4%BA%8C%E5%8F%89%E6%A0%91)
* [3.InvertBinaryTree（翻转二叉树）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/Tree.md#3invertbinarytree%E7%BF%BB%E8%BD%AC%E4%BA%8C%E5%8F%89%E6%A0%91)
* [4.BalancedBinaryTree（平衡二叉树判断）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/Tree.md#4balancedbinarytree%E5%B9%B3%E8%A1%A1%E4%BA%8C%E5%8F%89%E6%A0%91%E5%88%A4%E6%96%AD)
* [5.DiameterOfBinaryTree（二叉树的直径）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/Tree.md#5diameterofbinarytree%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E7%9B%B4%E5%BE%84)
* [6.PathSum（路径总和）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/Tree.md#6pathsum%E8%B7%AF%E5%BE%84%E6%80%BB%E5%92%8C)
* [7.PathSumIII（路径总和 3）]()
* [8.LongestUniValuePath（最长同值路径）]()
* [9.SecondMinimumNodeInABinaryTree（间隔遍历（打家劫舍 III））]()
* [10.SecondMinimumNodeInABinaryTree（二叉树中第二小的节点）]()

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
## 7.PathSumIII（路径总和 3）
问题描述：[LeetCode](https://leetcode-cn.com/problems/path-sum-iii/)   
代码：
``` java 
/**
 * 数据结构：树【递归】
 * leetcode:https://leetcode-cn.com/problems/path-sum-iii/
 * 题目描述：路径总和 3
 * */
public class PathSumIII {
    public int pathSum(TreeNode root, int sum) {
        if(root == null) return 0;
        int result =pathSumStartRoot(root,sum)+ pathSum(root.left,sum)+pathSum(root.right,sum);
        return result;
    }

    private int pathSumStartRoot(TreeNode root, int sum) {
        if(root == null) return 0;
        int result = 0;
        if(root.val == sum) result++;
        result += pathSumStartRoot(root.left,sum-root.val)+pathSumStartRoot(root.right,sum-root.val);
        return result;
    }
}
```

## 8.LongestUniValuePath（最长同值路径）
问题描述：[LeetCode](https://leetcode-cn.com/problems/longest-univalue-path/)   
代码：
``` java 
/**
 * 数据结构：树【递归】
 * leetcode:https://leetcode-cn.com/problems/longest-univalue-path/
 * 题目描述：最长同值路径
 * */
public class LongestUniValuePath {
    private int path = 0;
    public int longestUnivaluePath(TreeNode root) {
        dfs(root);
        return path;
    }
    private int dfs(TreeNode root) {
        if(root == null) return 0;
        int l = dfs(root.left);
        int r = dfs(root.right);
        int lPath = 0,rPath = 0;
        if(root.left != null && root.left.val == root.val){
            lPath = l + 1;
        }
        if(root.right != null && root.right.val == root.val){
            rPath = r + 1;
        }
        path = Math.max(path,lPath+rPath);
        return Math.max(lPath,rPath);
    }
}
```
## 9.SecondMinimumNodeInABinaryTree（间隔遍历（打家劫舍 III））
问题描述：[LeetCode](https://leetcode-cn.com/problems/house-robber-iii/)   
代码：
``` java 
/**
 * 数据结构：树【递归】
 * leetcode:https://leetcode-cn.com/problems/house-robber-iii/
 * 题目描述：间隔遍历（打家劫舍 III）
 * */
public class HouseRobberIII {
    public int rob(TreeNode root) {
        if (root == null) return 0;
        int val1 = root.val;
        if(root.left != null) val1 += rob(root.left.left) + rob(root.left.right);
        if(root.right != null) val1 += rob(root.right.left) + rob(root.right.right);
        int val2 = rob(root.left) + rob(root.right);
        return Math.max(val1,val2);
    }
}
```
## 10.SecondMinimumNodeInABinaryTree（二叉树中第二小的节点）
问题描述：[LeetCode](https://leetcode-cn.com/problems/second-minimum-node-in-a-binary-tree/)   
代码：
``` java 
/**
 * 数据结构：树【递归】
 * leetcode:https://leetcode-cn.com/problems/second-minimum-node-in-a-binary-tree/
 * 题目描述：二叉树中第二小的节点
 * */

public class SecondMinimumNodeInABinaryTree {
    public int findSecondMinimumValue(TreeNode root) {
        if(root == null) return -1;
        if(root.left == null && root.right == null) return -1;
        int lv = root.left.val;
        int rv = root.right.val;
        if(lv == root.val) lv = findSecondMinimumValue(root.left);
        if(rv == root.val) rv = findSecondMinimumValue(root.right);
        if(lv != -1 && rv != -1) return Math.min(lv,rv);
        if(lv != -1) return lv;
        if(rv != -1) return rv;
        return -1;
    }
}
```

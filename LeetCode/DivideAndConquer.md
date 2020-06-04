# 分治算法
* [1. 为运算表达式设计优先级（给表达式加括号）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/DivideAndConquer.md#1-%E4%B8%BA%E8%BF%90%E7%AE%97%E8%A1%A8%E8%BE%BE%E5%BC%8F%E8%AE%BE%E8%AE%A1%E4%BC%98%E5%85%88%E7%BA%A7%E7%BB%99%E8%A1%A8%E8%BE%BE%E5%BC%8F%E5%8A%A0%E6%8B%AC%E5%8F%B7)
* [2.FindSmallestLetterGreaterThanTarget(寻找比目标字母大的最小字母)]()

## 1. 为运算表达式设计优先级（给表达式加括号）
问题描述：[LeedCode](https://leetcode-cn.com/problems/different-ways-to-add-parentheses/description/)   
解决代码：
``` java
import java.util.ArrayList;
import java.util.List;

/**
 * 分治算法
 * leetcode:https://leetcode-cn.com/problems/different-ways-to-add-parentheses/description/
 * 为运算表达式设计优先级（给表达式加括号）
 * */
public class DifferentWaysToAddParentheses {
    public List<Integer> diffWaysToComputer(String input){
        List<Integer> ways = new ArrayList<>();
        for(int i =0 ; i<input.length();i++){
            char c = input.charAt(i);
            //题目规定：有效的运算符
            if(c == '+' || c == '-' || c == '*'){
                List<Integer> left = diffWaysToComputer(input.substring(0,i));
                List<Integer> right = diffWaysToComputer(input.substring(i+1));
                for(int first : left){
                    for (int last : right){
                        switch (c){
                            case '+':
                                ways.add(first+last);
                                break;
                            case '-':
                                ways.add(first-last);
                                break;
                            case '*':
                                ways.add(first*last);
                                break;
                        }
                    }
                }
            }
        }
        if(ways.size() == 0){
            ways.add(Integer.valueOf(input));
        }
        return ways;
    }
    /**
     * 测试
     * */
    public static void main(String[] args){
        DifferentWaysToAddParentheses diffWays = new DifferentWaysToAddParentheses();
        String input = "2-1-1*1+2";
        System.out.println(diffWays.diffWaysToComputer(input));
    }
}
```

## 2. UniqueBinarySearchTreesII(不同的二叉搜索树 II)
问题描述：[LeedCode](https://leetcode-cn.com/problems/unique-binary-search-trees-ii/)   
解决代码：
``` java
/**
 * 分治算法
 * leetcode:https://leetcode-cn.com/problems/unique-binary-search-trees-ii/
 * 不同的二叉搜索树 II
 * */
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode() {}
    TreeNode(int val) { this.val = val; }
    TreeNode(int val, TreeNode left, TreeNode right) {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}
public class UniqueBinarySearchTreesII {
    public List<TreeNode> generateTrees(int n) {
        if(n < 1){
            return new LinkedList<TreeNode>();
        }
        return generateSubtrees(1,n);
    }

    public List<TreeNode> generateSubtrees(int l,int r){
        List<TreeNode> result = new LinkedList<TreeNode>();
        if(l > r){
            result.add(null);
            return result;
        }
        for(int i = l;i <= r;++i){
            List<TreeNode> leftSubtrees = generateSubtrees(l,i-1);
            List<TreeNode> rightSubtrees = generateSubtrees(i+1,r);
            for(TreeNode left : leftSubtrees){
                for(TreeNode right : rightSubtrees){
                    TreeNode root = new TreeNode(i);
                    root.left = left;
                    root.right = right;
                    result.add(root);
                }
            }
        }
        return result;
    }
```

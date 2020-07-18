# 位运算

* [1.ContainsDuplicate（判断是否存在重复元素）]()
* [1.ContainsDuplicate（判断是否存在重复元素）]()
* [1.ContainsDuplicate（判断是否存在重复元素）]()
* [1.ContainsDuplicate（判断是否存在重复元素）]()

## 1.HammingDistance（统计两个数的二进制表示有多少位不同）
问题描述：[LeetCode](https://leetcode-cn.com/problems/hamming-distance/)   
代码：
``` java 
/**
 * 数据结构：位运算
 * leetcode：https://leetcode-cn.com/problems/hamming-distance/
 * 题目描述：Hamming Distance 统计两个数的二进制表示有多少位不同
 * */
public class HammingDistance {
    //方法1：先进行异或，结果多少个1就有多少位不同
    public int hammingDistance(int x, int y) {
        int z = x ^ y;
        int count = 0;
        while(z != 0){
            if( (z&1) == 1) count++;
            z = z >> 1;
        }
        return count;
    }
    //方法2：用Integer.bitCount统计1的个数
    public int hammingDistance1(int x, int y){
        return Integer.bitCount(x ^ y);
    }

}
```

## 2.MaximumDepthOfBinaryTree（二叉树的最大深度）
问题描述：[LeetCode](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)   
代码：
``` java 

```

## 3.MaximumDepthOfBinaryTree（二叉树的最大深度）
问题描述：[LeetCode](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)   
代码：
``` java 

```

## 4.MaximumDepthOfBinaryTree（二叉树的最大深度）
问题描述：[LeetCode](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)   
代码：
``` java 

```

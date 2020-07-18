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

## 2.MissingNumber（数组中缺失的那个数）
问题描述：[LeetCode](https://leetcode-cn.com/problems/missing-number/)   
代码：
``` java 
/**
 * 数据结构：位运算
 * leetcode：https://leetcode-cn.com/problems/missing-number/
 * 题目描述：数组中缺失的那个数
 * */
public class MissingNumber {
    //方法1：利用等差数列求缺失的值
    public int missingNumber(int[] nums) {
        int sum = 0;
        int l = nums.length;
        for (int i = 0; i < l; i++) {
            sum += nums[i];
        }
        return l*(l+1)/2 - sum;
    }

    //方法2：利用位运算---> a ^ b ^ a = b 下标+长度 和 原数组 异或
    /**eg: [4,5,3,2,1,0,7,8]
     * ->  4^0 ^ 5^1 ^ 3^2 ^ 2^3 ^ 1^4 ^ 0^5 ^ 7^6 ^ 8^7 ^ 8
     * ->  0^0 ^ 1^1 ^ 2^2 ^ 3^3 ^ 4^4 ^ 5^5 ^ 7^7 ^ 8^8 ^ 6
     * ->  0 ^ 0 ^ 0 ^ 0 ^ 0 ^ 0 ^ 0 ^ 0 ^ 6
     * ->  6
     * */
    public int missingNumber2(int[] nums){
        int result = 0;
        for (int i = 0; i < nums.length; i++) {
            result = result ^ i ^ nums[i];
        }
        return result ^ nums.length;
    }
}
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

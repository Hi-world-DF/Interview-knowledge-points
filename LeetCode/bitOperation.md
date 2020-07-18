# 位运算

* [1.HammingDistance（统计两个数的二进制表示有多少位不同）]()
* [2.MissingNumber（数组中缺失的那个数）]()
* [3.SingleNumber（数组中唯一的单一元素）]()
* [4.SingleNumberIII（数组中唯一的单一元素）]()

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

## 3.SingleNumber（数组中唯一的单一元素）
问题描述：[LeetCode](https://leetcode-cn.com/problems/single-number/)   
代码：
``` java 
/**
 * 数据结构：位运算
 * leetcode：https://leetcode-cn.com/problems/single-number/
 * 题目描述：数组中唯一的单一元素
 * */
public class SingleNumber {
    public int singleNumber(int[] nums) {
        int result = 0;
        for(int n : nums){
            result = n ^ result;
        }
        return result;
    }
}
```

## 4.SingleNumberIII（数组中唯一的单一元素）
问题描述：[LeetCode](https://leetcode-cn.com/problems/single-number-iii/)   
代码：
``` java 
import java.util.HashMap;

/**
 * 数据结构：位运算
 * leetcode：https://leetcode-cn.com/problems/single-number-iii/
 * 题目描述：数组中唯一的单一元素
 * */
public class SingleNumberIII {
    //方法1：利用hashMap
    public int[] singleNumber(int[] nums) {
        HashMap<Integer,Integer> hashMap = new HashMap();
        for(int n : nums){
            hashMap.put(n,hashMap.getOrDefault(n,0)+1);
        }
        int[] result = new int[2];
        int index = 0;
//        for(HashMap.Entry<Integer,Integer> item : hashMap.entrySet()){
//            if(item.getValue() == 1) {
//                result[index] = item.getKey();
//                index++;
//            }
//        }
        for(int n : hashMap.keySet()){
            if(hashMap.get(n) == 1){
                result[index] = n;
                index ++;
            }
        }
        return result;
    }

    //方法2：位运算
    public int[] singleNumber2(int[] nums) {
        int two = 0;
        for(int n : nums){
            two = two ^ n;
        }
        two = two & (-two);
        int[] result = new int[2];
        for (int n:nums) {
            if((n & two) == 0) {
                result[0] = result[0]^n;
            }else {
                result[1] = result[1]^n;
            }
        }
        return result;
    }
}
```

# 贪心算法
* [1.AssignCookies(饼干分配问题)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/greedyAlgorithm.md#1assigncookies%E9%A5%BC%E5%B9%B2%E5%88%86%E9%85%8D%E9%97%AE%E9%A2%98)
* [2.NonOverlappingIntervals(不重叠区间个数)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/greedyAlgorithm.md#2nonoverlappingintervals%E4%B8%8D%E9%87%8D%E5%8F%A0%E5%8C%BA%E9%97%B4%E4%B8%AA%E6%95%B0)
* [3.ReconstructionByHeight(按身高重排序)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/greedyAlgorithm.md#3reconstructionbyheight%E6%8C%89%E8%BA%AB%E9%AB%98%E9%87%8D%E6%8E%92%E5%BA%8F)
* [4.MinimumNumberOfArrowsToBurstBalloons(最少的箭引爆所有气球)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/greedyAlgorithm.md#4minimumnumberofarrowstoburstballoons%E6%9C%80%E5%B0%91%E7%9A%84%E7%AE%AD%E5%BC%95%E7%88%86%E6%89%80%E6%9C%89%E6%B0%94%E7%90%83)
* [5.BestTimeToBuyAndSellStock(买卖股票的最佳时期)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/greedyAlgorithm.md#5besttimetobuyandsellstock%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%9F)
* [6.BestTimeToBuyAndSellStock ii (买卖股票的最佳时期 2)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/greedyAlgorithm.md#6besttimetobuyandsellstock-ii-%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%9F-2)
* [7.CanPlaceFlowers (能否再种下n朵花)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/greedyAlgorithm.md#7canplaceflowers-%E8%83%BD%E5%90%A6%E5%86%8D%E7%A7%8D%E4%B8%8Bn%E6%9C%B5%E8%8A%B1)
* [8.IsSubsequence (判断子序列)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/greedyAlgorithm.md#8issubsequence-%E5%88%A4%E6%96%AD%E5%AD%90%E5%BA%8F%E5%88%97)
* [9.NonDecreasingArray (非递减序列)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/greedyAlgorithm.md#9nondecreasingarray-%E9%9D%9E%E9%80%92%E5%87%8F%E5%BA%8F%E5%88%97)
* [10.MaximumSubarray (最大子序列和)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/greedyAlgorithm.md#10maximumsubarray-%E6%9C%80%E5%A4%A7%E5%AD%90%E5%BA%8F%E5%88%97%E5%92%8C)
## 1.AssignCookies(饼干分配问题)
问题描述：[LeedCode](https://leetcode-cn.com/problems/assign-cookies/)  
解决代码：
``` java
package greedyAlgorithm;

import java.util.Arrays;

/**
 * 贪心算法
 * leetcode:https://leetcode-cn.com/problems/assign-cookies/
 * 饼干分配问题
 * */
public class AssignCookies {
    public int findContentChildren(int[] g, int[] s) {
        if(g == null || s == null){
            return 0;
        }
        Arrays.sort(g);
        Arrays.sort(s);
        int gi = 0, si = 0;
        while(gi < g.length && si < s.length){
            if(s[si] >= g[gi] ){
                gi++;
                si++;
            }else{
                si++;
            }
        }
        return gi;
    }
    /**
     * 测试
     * */
    public static void main(String[] args){
        int[] g = {1,2,4};
        int[] s = {1,1,2,1,3};
        AssignCookies ac = new AssignCookies();
        int a = ac.findContentChildren(g,s);
        System.out.println("可以满足的孩子个数："+a);
    }
}
```

## 2.NonOverlappingIntervals(不重叠区间个数)  
问题描述：[LeedCode](https://leetcode-cn.com/problems/non-overlapping-intervals/description/)   
解决代码：
``` java
package greedyAlgorithm;

import java.util.Arrays;
import java.util.Comparator;

/**
 * 贪心算法
 * leetcode:https://leetcode-cn.com/problems/non-overlapping-intervals/description/
 * 不重叠的区间个数
 * */

public class NonOverlappingIntervals {
    public int eraseOverlapIntervals(int[][] intervals) {
        //二维数组，通过比较下标来判定下一个是否重叠
        if(intervals.length == 0){
            return 0;
        }
        //根据列排序
        Arrays.sort(intervals, Comparator.comparingInt(o -> o[1]));
        int dnum = 0;
        int end = intervals[0][1];
        for(int i = 1;i < intervals.length;i++){
            if(end <= intervals[i][0]){
                end = intervals[i][1];
                continue;
            }
            dnum++;
        }
        return dnum;
    }

    public static void main(String[] args){
        NonOverlappingIntervals noi = new NonOverlappingIntervals();
        int[][] intervals = {{1,2},{3,4},{2,6},{5,7},{7,9},{8,9}};
        int num = noi.eraseOverlapIntervals(intervals);
        System.out.println("需要移除区间个数："+num);
    }

}

```
## 3.ReconstructionByHeight(按身高重排序) 
问题描述：[LeedCode](https://leetcode-cn.com/problems/queue-reconstruction-by-height/)   
解决代码：
``` java
package greedyAlgorithm;

import java.lang.reflect.Array;
import java.util.*;

/**
 * 贪心算法
 * leetcode:https://leetcode-cn.com/problems/queue-reconstruction-by-height/
 * 根据身高重新排序
 * */
public class ReconstructionByHeight {
    public int[][] reconstructQueue(int[][] people) {
        Arrays.sort(people, new Comparator<int[]>() {
            @Override
            public int compare(int[] o1, int[] o2) {
                return o1[0]==o2[0]?o1[1] - o2[1]:o2[0] - o1[0];
            }
        });

        List<int[]> result =new ArrayList<>();
        for(int[] p : people) {
            result.add(p[1], p);
        }
        int num = people.length;
        return result.toArray(new int[num][2]);
    }
    public static void main(String[] args){
        ReconstructionByHeight rbh = new ReconstructionByHeight();
        int[][] p ={{7,0}, {4,4}, {7,1}, {5,0}, {6,1}, {5,2}};
        System.out.println("input:");
        for(int[] a : p){
            System.out.print(Arrays.toString(a)+" ");
        }
        int[][] a =rbh.reconstructQueue(p);
        System.out.println("\noutput:");
        for(int[] b : a){
            System.out.print(Arrays.toString(b)+" ");
        }
    }
}
```

## 4.MinimumNumberOfArrowsToBurstBalloons(最少的箭引爆所有气球)
问题描述：[LeedCode](https://leetcode-cn.com/problems/minimum-number-of-arrows-to-burst-balloons/description/)   
解决代码：
``` java
package greedyAlgorithm;

import java.util.Arrays;
import java.util.Comparator;
/**
 * 贪心算法
 * leetcode:https://leetcode-cn.com/problems/minimum-number-of-arrows-to-burst-balloons/description/
 * 最少的箭引爆所有气球
 * */
public class MinimumNumberOfArrowsToBurstBalloons {
    public int findMinArrowShots(int[][] points) {
        if(points.length == 0){
            return 0;
        }
        Arrays.sort(points, Comparator.comparingInt(o -> o[1]));
        int sum = 1;
        int b = points[0][1];
        for(int i = 1 ;i < points.length;i++){
            int pre = points[i][0];
            if(pre <= b){
                continue;
            }else{
                b = points[i][1];
                sum++;
            }
        }
        return sum;
    }

    public static void main(String[] args){
        MinimumNumberOfArrowsToBurstBalloons mnoatbb =new MinimumNumberOfArrowsToBurstBalloons();
        int[][] points = {{2,3},{1,5},{4,7},{8,9}};
        int num = mnoatbb.findMinArrowShots(points);
        System.out.println("最少需要 "+num+" 支箭");
    }
}
```
## 5.BestTimeToBuyAndSellStock(买卖股票的最佳时期)
问题描述：[LeedCode](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)   
解决代码：
``` java
/**
 * 贪心算法
 * leetcode:https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/
 * 买卖股票的最佳时期
 * */
public class BestTimeToBuyAndSellStock {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        int max = 0;
        if(n==0){
            return 0;
        }
        int min = prices[0];
        for(int i = 0;i<n;i++){
            if(prices[i]<min){
                min = prices[i];
            }else{
                max = max > (prices[i]-min)?max:(prices[i]-min);
            }
        }
        return max;
    }
    /**
     * main()测试
     * */
    public static void main(String[] args){
        BestTimeToBuyAndSellStock bttbass = new BestTimeToBuyAndSellStock();
        int[] p ={2,3,12,1,3,4};
        int output = bttbass.maxProfit(p);
        System.out.println("最大的收益利润："+output);
    }
}

```
## 6.BestTimeToBuyAndSellStock ii (买卖股票的最佳时期 2)
问题描述：[LeedCode](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/description/)   
解决代码：
``` java
/**
 * 贪心算法
 * leetcode:https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/description/
 * 买卖股票的最佳时期2
 * */
public class BestTimeToBuyAndSellStock2 {
    public int maxProfit(int[] prices) {
        int maxP = 0;
        int n = prices.length;
        for(int i = 1; i < n;i++){
            if(prices[i]>prices[i-1]){
                maxP += prices[i] -prices[i-1];
            }
        }
        return maxP;
    }
    /**
     * 测试
     * */
    public static void main(String[] args){
        int[] p = {1,2,7,3,5,2,6,7};
        BestTimeToBuyAndSellStock2 bttbass = new BestTimeToBuyAndSellStock2();
        int result = bttbass.maxProfit(p);
        System.out.println("最大的收益："+result);
    }
}
```

## 7.CanPlaceFlowers (能否再种下n朵花)
问题描述：[LeedCode](https://leetcode-cn.com/problems/can-place-flowers/)    
解决代码：
``` java
/**
 * 贪心算法
 * leetcode:https://leetcode-cn.com/problems/can-place-flowers/
 * 能否再种下n多花
 * */
public class CanPlaceFlowers {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int fNums = flowerbed.length;
        int fMax = 0;
        for(int i = 0;i < fNums;i++){
            if(flowerbed[i] == 1){
                continue;
            }
            int pre = (i==0) ? 0:flowerbed[i-1];
            int next = (i==fNums-1)? 0:flowerbed[i+1];
            if(pre == 0 && next == 0){
                fMax++;
                flowerbed[i] = 1;
            }
        }
        return n <= fMax;
    }
    /**
    *测试
    */
    public static void main(String[] args ){
        CanPlaceFlowers cpf = new CanPlaceFlowers();
        int n = 1;
        int[] flowerbed = {1,0,1,0,1,0};
        boolean result = cpf.canPlaceFlowers(flowerbed,n);
        System.out.println("是否可以种下n朵花"+result);
    }
}

```
## 8.IsSubsequence (判断子序列)
问题描述：[LeedCode](https://leetcode-cn.com/problems/is-subsequence/)   
解决代码：
``` java
/**
 * 贪心算法
 * leetcode:https://leetcode-cn.com/problems/is-subsequence/
 * 判断是否是子序列
 * */
public class IsSubsequence {
    public static boolean isSubsequence(String s,String t) {
//        int si = s.length();
//        int ti = t.length();
//        for (int i = 1, j = 1; i < ti && j <= si;) {
//            if (t.charAt(i) == s.charAt(j)) {
//                j++;
//            }
//            i++;
//            if (j > si) {
//                return true;
//            }
//        }
//        return false;
        int index = -1;
        /**循环比较s中的字符
         *s.toCharArray()将s字符串转换为字符数组
         */
        for(char c : s.toCharArray()){
            /**
             * 没找到，返回-1
             * 1.int indexOf(String str):
             *      返回第一次出现的指定子字符串在此字符串中的索引
             * 2.int indexOf(String str, int startIndex):
             *      从指定的索引处开始，返回第一次出现的指定子字符串在此字符串中的索引
             * 3.int lastIndexOf(String str):
             *      返回在此字符串中最右边出现的指定子字符串的索引
             * 4.int lastIndexOf(String str, int startIndex):
             *      从指定的索引处开始向后搜索，返回在此字符串中最后一次出现的指定子字符串的索引
             * */
            index = t.indexOf(c,index+1);
            if(index == -1){
                return false;
            }
        }
        return true;
    }
    public static void main(String[] args){
        String s = "abc";
        String t = "ahbgc";
        boolean result = IsSubsequence.isSubsequence(s,t);
        System.out.println(result);
    }
}
```

## 9.NonDecreasingArray (非递减序列)
问题描述：[LeedCode](https://leetcode-cn.com/problems/non-decreasing-array/)   
解决代码：
``` java
/**
 * 贪心算法
 * leetcode:https://leetcode-cn.com/problems/non-decreasing-array/
 * 非递减序列
 * */
public class NonDecreasingArray {
    public boolean hasDecreasingArray(int[] nums){
        int n = nums.length;
        //a用来计数，只能修改 1 个数使的数组变为非递减
        int a = 0;
        for (int i = 1;i < n;i++){
            if(nums[i] >= nums[i-1]){
                continue;
            }
            a++;
            if(i-2>=0 && nums[i-2]>nums[i]){
                nums[i]=nums[i-1];
            }else{
                nums[i-1]=nums[i];
            }
        }
        //当不需要改数字或者只需改一次，则为true，否则为false
        return a<=1;
    }
    /**
     * 测试
     * */
    public static void main(String[] args){
        int[] nums ={1,1,1};
        NonDecreasingArray nonDecreasingArray = new NonDecreasingArray();
        boolean result = nonDecreasingArray.hasDecreasingArray(nums);
        System.out.println(result);
    }
}

```

## 10.MaximumSubarray (最大子序列和)
问题描述：[LeedCode](https://leetcode-cn.com/problems/maximum-subarray/)   
解决代码：
``` java
/**
 * 贪心算法
 * leetcode:https://leetcode-cn.com/problems/maximum-subarray/description/
 * 子数组最大和
 * */
public class MaximumSubarray {
    public int maximumSubarray(int[] nums){
        int n = nums.length;
        if(n == 0 || nums ==null){
            return 0;
        }
        int preIndex = nums[0];
        int maxSum = preIndex;
        for(int i = 1;i < n;i++){
            preIndex = preIndex>0?preIndex+nums[i]:nums[i];
            maxSum = maxSum > preIndex?maxSum:preIndex;
        }
        return maxSum;
    }
    /**
     * 测试
     * */
    public static void main(String[] args){
        int[] nums = {-2,1,-3,4,-1,2,1,-5,4};
        MaximumSubarray m = new MaximumSubarray();
        int result = m.maximumSubarray(nums);
        System.out.println(result);
    }
}
```

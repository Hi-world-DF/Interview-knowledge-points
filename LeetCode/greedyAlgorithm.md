# 贪心算法
* [1.AssignCookies(饼干分配问题)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/greedyAlgorithm.md#1assigncookies%E9%A5%BC%E5%B9%B2%E5%88%86%E9%85%8D%E9%97%AE%E9%A2%98)
* [2.NonOverlappingIntervals(不重叠区间个数)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/greedyAlgorithm.md#2nonoverlappingintervals%E4%B8%8D%E9%87%8D%E5%8F%A0%E5%8C%BA%E9%97%B4%E4%B8%AA%E6%95%B0)
* [3.ReconstructionByHeight(按身高重排序)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/greedyAlgorithm.md#3reconstructionbyheight%E6%8C%89%E8%BA%AB%E9%AB%98%E9%87%8D%E6%8E%92%E5%BA%8F)
* [4.MinimumNumberOfArrowsToBurstBalloons(最少的箭引爆所有气球)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/greedyAlgorithm.md#4minimumnumberofarrowstoburstballoons%E6%9C%80%E5%B0%91%E7%9A%84%E7%AE%AD%E5%BC%95%E7%88%86%E6%89%80%E6%9C%89%E6%B0%94%E7%90%83)
* [5.BestTimeToBuyAndSellStock(买卖股票的最佳时期)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/greedyAlgorithm.md#5besttimetobuyandsellstock%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%9F)
* [6.BestTimeToBuyAndSellStock ii (买卖股票的最佳时期 2)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/greedyAlgorithm.md#6besttimetobuyandsellstock-ii-%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%9F-2)

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

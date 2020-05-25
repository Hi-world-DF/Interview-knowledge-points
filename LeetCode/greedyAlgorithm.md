# 贪心算法
* [1.AssignCookies(饼干分配问题)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/greedyAlgorithm.md#1assigncookies%E9%A5%BC%E5%B9%B2%E5%88%86%E9%85%8D%E9%97%AE%E9%A2%98)
* [2.NonOverlappingIntervals(不重叠区间个数)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/greedyAlgorithm.md#2nonoverlappingintervals%E4%B8%8D%E9%87%8D%E5%8F%A0%E5%8C%BA%E9%97%B4%E4%B8%AA%E6%95%B0)
* [2.NonOverlappingIntervals(不重叠区间个数)]()


## 1.AssignCookies(饼干分配问题)
问题描述：[LeedCode]()解决代码：
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
问题描述：[LeedCode]()解决代码：
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

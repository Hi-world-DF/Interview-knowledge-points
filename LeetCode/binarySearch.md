# 二分查找
* [1. SqrtX（求开方）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/binarySearch.md#1-sqrtx%E6%B1%82%E5%BC%80%E6%96%B9)


## 1. SqrtX(求开方)
问题描述：[LeedCode](https://leetcode-cn.com/problems/sqrtx/description/)   
解决代码：
``` java
import java.util.Scanner;

/**
 * 二分查找
 * leetcode:https://leetcode-cn.com/problems/sqrtx/description/
 * X的平方根
 * */
public class SqrtX {
    public int mySqrt(int x){
        if(x <= 1){
            return x;
        }
        int first = 1;
        int last = x;
        while(first <= last){
            int mid = first+(last-first)/2;
            int sqrt = x/mid;
            if(sqrt == mid){
                return mid;
            }else if(sqrt < mid){
                last = mid-1;
            }else{
                first = mid+1;
            }
        }
        return last;
    }
    /**
     * 测试
     * */
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        int x = in.nextInt();
        SqrtX sqrtX = new SqrtX();
        int result = sqrtX.mySqrt(x);
        System.out.println(result);
    }
}
```

## 2.AssignCookies(饼干分配问题)
问题描述：[LeedCode](https://leetcode-cn.com/problems/assign-cookies/)   
解决代码：

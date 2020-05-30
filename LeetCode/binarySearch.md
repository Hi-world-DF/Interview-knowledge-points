# 二分查找
* [1. SqrtX（求开方）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/binarySearch.md#1-sqrtx%E6%B1%82%E5%BC%80%E6%96%B9)
* [2.FindSmallestLetterGreaterThanTarget(寻找比目标字母大的最小字母)]()

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

## 2.FindSmallestLetterGreaterThanTarget(寻找比目标字母大的最小字母)
问题描述：[LeedCode](https://leetcode-cn.com/problems/find-smallest-letter-greater-than-target/)   
解决代码：
``` java
/**
 * 二分查找
 * leetcode:https://leetcode-cn.com/problems/find-smallest-letter-greater-than-target/
 * 寻找比目标字母大的最小字母
 * */
public class FindSmallestLetterGreaterThanTarget {
    public char nextGreatestLetter(char[] letters, char target) {
        int n = letters.length;
        int first = 0;
        int last = n-1;
        while(first <= last){
            int mid = (last + first)/2;
            if(letters[mid] <= target){
                first = mid + 1;
            }else{
                last = mid -1;
            }
        }

        if(first < n){
            //说明可以在letters[]中找到
            return letters[first];
        }else{
            //没找到就返回letters[]第一个元素
            return letters[0];
        }

    }
    /**
     * 测试
     * */
    public static void main(String[] args){
        char[] letters = {'c','f','j'};
        char target = 'i';
        FindSmallestLetterGreaterThanTarget f = new FindSmallestLetterGreaterThanTarget();
        char result = f.nextGreatestLetter(letters,target);
        System.out.println(result);
    }
}
```

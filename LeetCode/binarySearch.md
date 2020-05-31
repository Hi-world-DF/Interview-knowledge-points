# 二分查找
* [1. SqrtX（求开方）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/binarySearch.md#1-sqrtx%E6%B1%82%E5%BC%80%E6%96%B9)
* [2.FindSmallestLetterGreaterThanTarget(寻找比目标字母大的最小字母)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/binarySearch.md#2findsmallestlettergreaterthantarget%E5%AF%BB%E6%89%BE%E6%AF%94%E7%9B%AE%E6%A0%87%E5%AD%97%E6%AF%8D%E5%A4%A7%E7%9A%84%E6%9C%80%E5%B0%8F%E5%AD%97%E6%AF%8D)

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

## 3.SingleElementInASortedArray(有序数组中的单一元素)
问题描述：[LeedCode](https://leetcode-cn.com/problems/single-element-in-a-sorted-array/description/)   
解决代码：
``` java
/**
 * 二分查找
 * leetcode:https://leetcode-cn.com/problems/single-element-in-a-sorted-array/description/
 * 有序数组中的单一元素
 * */
public class SingleElementInASortedArray {
    public int singleNonDuplicate(int[] nums){
        /**
         * 方法一：没有使用二分法，直接遍历整个数组
         * */
//        int n = nums.length;
//        for(int i = 0;i < n;i++){
//            if(nums[i] == nums[i+1]){
//                i++;
//                continue;
//            }
//            return nums[i];
//        }
//        return nums[n-1];
        /**
         * 方法二：使用二分法（有点牵强，但是时间复杂度低）
         * */
        int first = 0;
        int last = nums.length -1;
        while(first < last){
            int mid = (first+last)/2;
            if(mid%2==1){
                //这里保证mid、first、last都是偶数
                mid--;
            }
            //如果nums[mid] == nums[mid+1]则这个单数在后半部分；否则在前半部分
            if(nums[mid] == nums[mid+1]){
                first = mid + 2;
            }else{
                last = mid;
            }
        }
        return nums[first];
    }
    /**
     * 测试
     * */
    public static void main(String[] args){
        SingleElementInASortedArray s =new SingleElementInASortedArray();
        int[] nums = {1,1,2,3,3,4,4,8,8};
        int result = s.singleNonDuplicate(nums);
        System.out.println(result);
    }
}
```

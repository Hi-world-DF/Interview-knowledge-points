# 双指针问题
* [1.TwoNumSum(有序数组的两数相加)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/doublePointerProblem.md#1twonumsum%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E4%B8%A4%E6%95%B0%E7%9B%B8%E5%8A%A0)
* [2.SumOfSquareNumbers(两数平方和)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/doublePointerProblem.md#2sumofsquarenumbers%E4%B8%A4%E6%95%B0%E5%B9%B3%E6%96%B9%E5%92%8C)
* [3.ReverseVowelsOfString(反转字符串中的元音字符)](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/doublePointerProblem.md#3reversevowelsofstring%E5%8F%8D%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2%E4%B8%AD%E7%9A%84%E5%85%83%E9%9F%B3%E5%AD%97%E7%AC%A6)

## 1.TwoNumSum(有序数组的两数相加)
问题描述：[LeedCode](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/)  
代码：
``` java
/**
 * 双指针问题
 * leetcode:https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/
 * 两数相加问题
 * */

public class AddTwoNumbers {
    public static int[] twoSum(int[] numbers, int target) {
        if(numbers == null){
            return null;
        }
        //定义两个指针，一个指向数组第一个元素，一个指向数组最后一个元素
        int i = 0;
        int j = numbers.length -1;
        while(i<j){
            int sum = numbers[i] + numbers[j];
            if(sum == target){
                return new int[]{i+1,j+1};
            }else if(sum < target){
                i++;
            }else{
                j--;
            }
        }
        return null;
    }
    /**
     * 测试
     * */
    public static void main(String[] args){
        int[] numbers = {2,7,11,15};
        int target = 9;
        int[] result = twoSum(numbers,target);
        for (int i = 0;i < result.length;i++){
            System.out.print(result[i]+" ");
        }
    }

}
```

## 2.SumOfSquareNumbers(两数平方和)
问题描述：[LeedCode](https://leetcode-cn.com/problems/sum-of-square-numbers/)  
代码：
``` java
class Solution {
    public boolean judgeSquareSum(int c) {
        int i =0;
        int j =(int) Math.sqrt(c);
        while(i<=j){
            int sum = i*i+j*j;
            if(sum == c){
                return true;
            }else if(sum < c){
                i++;
            }else{
                j--;
            }
        }
        return false;
    }
}
```

## 3.ReverseVowelsOfString(反转字符串中的元音字符)
问题描述：[LeedCode](https://leetcode-cn.com/problems/reverse-vowels-of-a-string/)  
代码：
``` java
class Solution {
    public String reverseVowels(String s) {
        //使用hashSet存储元音字符
        HashSet<Character> vowels = new HashSet<>(Arrays.asList('a','e','i','o','u','A','E','I','O','U'));
        if(s == null){
            return null;
        }
        //定义两个指针，一个指向S第一个元素，一个指向S最后一个元素
        int i = 0;
        int j = s.length()-1;
        //用一个数组来存放result（反转元音字母之后的）结果
        char[] result =new char[s.length()];
        while(i<=j){
            char front = s.charAt(i);
            char last = s.charAt(j);
            if(!vowels.contains(front)){
                result[i] = front;
                i++;
            }else if(!vowels.contains(last)){
                result[j] = last;
                j--;
            }else{
                result[i] = last;
                result[j] = front;
                i++;
                j--;
            }
        }
        return new String(result);
    }
}
```
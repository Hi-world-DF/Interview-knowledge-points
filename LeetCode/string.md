# 字符串
* [1.ValidAnagram（两个字符串所包含的字符是否完全相同）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/string.md#1validanagram%E4%B8%A4%E4%B8%AA%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%89%80%E5%8C%85%E5%90%AB%E7%9A%84%E5%AD%97%E7%AC%A6%E6%98%AF%E5%90%A6%E5%AE%8C%E5%85%A8%E7%9B%B8%E5%90%8C)
* [2.LongestPalindrome（可以构成的最长的回文串）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/string.md#2longestpalindrome%E5%8F%AF%E4%BB%A5%E6%9E%84%E6%88%90%E7%9A%84%E6%9C%80%E9%95%BF%E7%9A%84%E5%9B%9E%E6%96%87%E4%B8%B2)

## 1.ValidAnagram（两个字符串所包含的字符是否完全相同）
问题描述：[LeetCode](https://leetcode-cn.com/problems/valid-anagram/)   
代码：
``` java 
import java.util.Arrays;
/**
 * 数据结构：字符串
 * leetcode：https://leetcode-cn.com/problems/valid-anagram/
 * 两个字符串所包含的字符是否完全相同
 * */
public class ValidAnagram {
    //方法一：转换为字符数组，然后排序，最后比较
    public boolean isAnagram(String s, String t) {
        if(s.length() != t.length()){
            return false;
        }
        char[] str1 = s.toCharArray();
        char[] str2 = t.toCharArray();
        Arrays.sort(str1);
        Arrays.sort(str2);
        return Arrays.equals(str1,str2);
    }

    //方法二：HashMap
    public boolean isAnagram1(String s,String t){
        if(s.length() != t.length()){
            return false;
        }
        int[] counter = new int[26];
        for(int i = 0;i < s.length();i++){
            counter[s.charAt(i) - 'a']++;
            counter[t.charAt(i) - 'b']--;
        }
        for(int c : counter){
            if(c != 0){
                return false;
            }
        }
        return true;
    }
}
```
## 2.LongestPalindrome（可以构成的最长的回文串）
问题描述：[LeetCode](https://leetcode-cn.com/problems/longest-palindrome/)    
代码：
``` java 
import java.util.HashMap;
/**
 * 数据结构：字符串
 * leetcode：https://leetcode-cn.com/problems/longest-palindrome/
 * 可以构成的最长的回文串
 * */
public class LongestPalindrome {
    //方法一：使用HashMap
    public int longestPalindrome(String s) {
        int result = 0;
        HashMap<Character,Integer> hashMap = new HashMap<>();
        for(char c : s.toCharArray()){
            char key = c;
            int value = 1;
            if(hashMap.get(key)!= null){
                value = hashMap.get(key) + 1;
            }
            hashMap.put(key,value);
        }
        for(char key : hashMap.keySet()){
            int value = hashMap.get(key);
            result = result + 2*(value/2);
        }
        if(result < s.length()){
            result++;
        }
        return result;
    }
    //方法二：利用数组来统计
    public int longestPalindrome1(String s) {
        int[] nums = new int[256];
        int result = 0;
        for(char c : s.toCharArray()){
            nums[c]++;
        }
        for(int num : nums){
            result += 2*(num/2);
        }
        if(result < s.length()){
            result = result + 1;
        }
        return result;
    }
}
```

# 哈希表 HashMap.HashSet.HashTable
* [1.ContainsDuplicate（判断是否存在重复元素）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/HashMap.md#1containsduplicate%E5%88%A4%E6%96%AD%E6%98%AF%E5%90%A6%E5%AD%98%E5%9C%A8%E9%87%8D%E5%A4%8D%E5%85%83%E7%B4%A0)
* [2.TwoSum（两数之和）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/HashMap.md#2twosum%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C)
* [3.LongestConsecutiveSequence（最长连续序列）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/HashMap.md#3longestconsecutivesequence%E6%9C%80%E9%95%BF%E8%BF%9E%E7%BB%AD%E5%BA%8F%E5%88%97)
* [4.LongestHarmoniousSubsequence（最长和谐子序列）](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/LeetCode/HashMap.md#4longestharmonioussubsequence%E6%9C%80%E9%95%BF%E5%92%8C%E8%B0%90%E5%AD%90%E5%BA%8F%E5%88%97)

## 1.ContainsDuplicate（判断是否存在重复元素）
问题描述：[LeetCode](https://leetcode-cn.com/problems/contains-duplicate/)   
代码：
``` java 
import java.util.HashMap;
import java.util.HashSet;

/**
 * 数据结构：哈希表
 * leetcode:https://leetcode-cn.com/problems/contains-duplicate/
 * 问题描述：判断是否存在重复元素
 * */
public class ContainsDuplicate {
    //方法一：HashMap
    public boolean containsDuplicate(int[] nums) {
        HashMap<Integer,Integer> hashMap = new HashMap<>();
        for(int i = 0;i < nums.length;i++){
            if(hashMap.containsKey(nums[i])){
                return true;
            }else{
                hashMap.put(nums[i],i);
            }
        }
        return false;
    }
    //方法二：HashSet
    public boolean containsDuplicate2(int[] nums) {
        HashSet<Integer> hashSet = new HashSet<>();
        for(int num : nums){
            hashSet.add(num);
        }
        if(hashSet.size() < nums.length){
            return true;
        }else{
            return false;
        }
    }

}
```

## 2.TwoSum（两数之和）
问题描述：[LeetCode](https://leetcode-cn.com/problems/two-sum/)   
代码：
``` java 
import java.util.HashMap;

/**
 * 数据结构：哈希表
 * leetcode:https://leetcode-cn.com/problems/two-sum/
 * 问题描述：两数之和
 * */
public class TwoSum {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer,Integer> hashMap = new HashMap<>();
        for(int i = 0;i < nums.length;i++){
            if(hashMap.containsKey(target - nums[i])){
                return new int[]{hashMap.get(target - nums[i]),i};
            }else{
                hashMap.put(nums[i],i);
            }
        }
        return null;
    }
}
```

## 3.LongestConsecutiveSequence（最长连续序列）
问题描述：[LeetCode](https://leetcode-cn.com/problems/longest-consecutive-sequence/)   
代码：
``` java 
import java.util.HashMap;

/**
 * 数据结构：哈希表
 * leetcode:https://leetcode-cn.com/problems/longest-consecutive-sequence/
 * 问题描述：最长连续序列
 * */
public class LongestConsecutiveSequence {
    public int longestConsecutive(int[] nums) {
        HashMap<Integer,Integer> hashMap = new HashMap<>();
        for(int num : nums){
            hashMap.put(num,1);
        }
        for(int num : nums){
            forWard(hashMap,num);
        }
        return maxCount(hashMap);
    }

    private int maxCount(HashMap<Integer, Integer> hashMap) {
        int max = 0;
        for(int num : hashMap.keySet()){
            max = Math.max(max,hashMap.get(num));
        }
        return max;
    }

    private int forWard(HashMap<Integer, Integer> hashMap, int num) {
        if(!hashMap.containsKey(num)){
            return 0;
        }
        int currentValue = hashMap.get(num);
        if(currentValue > 1){
            return currentValue;
        }
        currentValue = forWard(hashMap,num+1)+1;
        hashMap.put(num,currentValue);
        return currentValue;
    }
}
```
## 4.LongestHarmoniousSubsequence（最长和谐子序列）
问题描述：[LeetCode](https://leetcode-cn.com/problems/longest-harmonious-subsequence/)   
代码：
``` java 
import java.util.HashMap;

/**
 * 数据结构：哈希表
 * leetcode:https://leetcode-cn.com/problems/longest-harmonious-subsequence/
 * 问题描述：最长和谐子序列
 * */
public class LongestHarmoniousSubsequence {
    public int findLHS(int[] nums) {
        int max = 0;
        HashMap<Integer,Integer> hashMap = new HashMap<>();
        for(int i = 0;i < nums.length;i++){
            hashMap.put(nums[i],hashMap.getOrDefault(nums[i], 0) + 1);
        }
        for(int num : hashMap.keySet()){
            if(hashMap.containsKey(num+1)){
                int sum = hashMap.get(num) + hashMap.get(num+1);
                max = Math.max(max,sum);
            }
        }
        return max;
    }
}
```

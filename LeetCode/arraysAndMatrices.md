# 数组和矩阵
* [1.MaxConsecutiveOnes（最大连续1的个数）]()

## 1.MaxConsecutiveOnes（最大连续1的个数）
问题描述：[LeetCode](https://leetcode-cn.com/problems/max-consecutive-ones/)   
代码：
``` java 
/**
 * 数据结构：数组和矩阵
 * leetcode：https://leetcode-cn.com/problems/max-consecutive-ones/
 * 题目描述：最大连续1的个数
 * */
public class MaxConsecutiveOnes {
    public int findMaxConsecutiveOnes(int[] nums) {
        int max = 0;
        int current = 0;
        for(int num : nums){
            current = num == 0?0:current+1;
            max = Math.max(max,current);
            //max = max>current?max:current;
        }
        return max;
    }
    public static void main(String[] args){

    }
}
```
## 2.MoveZeroes（移动零到数组末尾）
问题描述：[LeetCode](https://leetcode-cn.com/problems/move-zeroes/)   
代码：
``` java 
/**
 * 数据结构：数组和矩阵
 * leetcode：https://leetcode-cn.com/problems/move-zeroes/
 * 题目描述：移动零到数组末尾
 * */
public class MoveZeroes {
    public void moveZeroes(int[] nums) {
        int n = nums.length;
        int notZero = 0;
        for(int i = 0; i < n;i++){
            if(nums[i] != 0){
                nums[notZero] = nums[i];
                notZero++;
            }
        }
        while(notZero < n){
            nums[notZero] = 0;
            notZero++;
        }
    }
}
```
## 3.ReshapeTheMatrix（重塑矩阵）
问题描述：[LeetCode](https://leetcode-cn.com/problems/reshape-the-matrix/)   
代码：
``` java 
/**
 * 数据结构：数组和矩阵
 * leetcode：https://leetcode-cn.com/problems/reshape-the-matrix/
 * 题目描述：重塑矩阵
 * */
public class ReshapeTheMatrix {
    public int[][] matrixReshape(int[][] nums, int r, int c) {
        int[][] result = new int[r][c];
        int m = nums.length;
        int n = nums[0].length;
        int[] num = new int[m*n];
        for(int i = 0,x=0;i < m;i++){
            for(int j = 0;j < n;j++){
                num[x] = nums[i][j];
                x++;
            }
        }
        for(int i = 0; i < num.length;i++){
            System.out.print(num[i]+" ");
        }
        System.out.println();
        if(m*n < r*c){
            return nums;
        }
        for(int i = 0,y=0;i < r;i++){
            for(int j = 0;j < c;j++){
                result[i][j] = num[y];
                y++;
            }
        }
        return result;
    }
}
```

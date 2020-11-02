[1.两数之和](https://leetcode-cn.com/problems/two-sum/)

# 题目描述

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

**示例:**

```
给定 nums = [2, 7, 11, 15], target = 9
因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

# 题解

两遍哈希表，时间复杂度O(n),空间复杂度O(n)

# 代码

```java
//Java
//执行用时：4ms
//内存消耗：39.3MB
public class Solution{
    public int[] twoSum(int[] nums, int target){
        //定义一个哈希表
        final HashMap<Integer, Integer> myMap = new HashMap<Integer, Integer>();
        //int[] result = new int[2];
        for(int i = 0; i < nums.length; i++){//遍历数组并初始化哈希表
            myMap.put(nums[i], i);
        }
        for(int i = 0; i < nums.length; i++){
            //第二次遍历数组，同时判断是否有符合要求的数据
            final Integer v = myMap.get(target - nums[i]);
            if(v != null && v > i){
                return new int[] {i, v};
            }
        }
        return null;
    }
};
```

```c++
//C++
//两遍哈希表
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int n = nums.size();
        unordered_map<int, int> myMap;
        for(int i = 0; i < n; i++){
            myMap[nums[i]] = i;
        }
        for(int i = 0; i < n; i++){
            if(myMap.find(target-nums[i]) != myMap.end() && myMap[target-nums[i]] != i){
                return {i, myMap[target-nums[i]]};
            }
        }
        return {};
    }
};
```
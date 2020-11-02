[15.三数之和](https://leetcode-cn.com/problems/3sum/)

# 题目描述

给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。

**示例:**

```
给定数组 nums = [-1, 0, 1, 2, -1, -4]，
满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

# 题解

暴力解法的时间复杂度为O(n³)，会超过题目时间限制。

使用排序+双指针方法，可以将算法的时间复杂度优化为O(n²)。

# 代码

```java
//Java
//执行用时：26ms
//内存消耗：42.6MB
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        int n = nums.length;
        Arrays.sort(nums);//对原数组排序
        List<List<Integer>> ans = new ArrayList<List<Integer>>();
        for(int first = 0; first < n; first++){
        //当first不是本轮循环第一个数，并且与前一个数相同时，为了避免重复，直接跳过当次循环
            if(first > 0 && nums[first] == nums[first-1]){
                continue;
            }
            int second = first + 1;//初始化second
            int third = n - 1;//初始化third
            int target = -nums[first];
            while(second < third){
                if(nums[second] + nums[third] == target){
                    List<Integer> list = new ArrayList<Integer>();
                    list.add(nums[first]);
                    list.add(nums[second]);
                    list.add(nums[third]);
                    ans.add(list);
                    second++;//注意在这里需要先对second和third进行更新，再进入while循环
                    third--;
                    while(second<third && nums[second] == nums[second-1]) second++;
                    while(second<third && nums[third] == nums[third+1]) third--;
                }else if(nums[second] + nums[third] > target){
                    third--;
                }else{
                    second++;
                }
            }
        }
        return ans;
    }
}
```

```c++
//C++
//执行用时：104ms
//内存消耗：19.6MB
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(), nums.end());//对原数组进行排序
        vector<vector<int>> ans;
        for(int first = 0; first < n; first++){
        //当first不是本轮循环第一个数，并且与前一个数相同时，为了避免重复，直接跳过当次循环
            if(first > 0 && nums[first] == nums[first - 1]){
                    continue;
            }
            int target = -nums[first];//second与third之和目标值
            int third = n - 1;//令third为数组最后一个数
            for(int second = first + 1; second < n; second++){
            //当second不是本轮循环第一个数，并且与前一个数相同时，为了避免重复，直接跳过当次循环
                if(second > first + 1 && nums[second] == nums[second - 1]){
                    continue;
                }
                while(second < third && nums[second] + nums[third] > target){
                    third--;
                }
                if(second == third){
                    break;
                }
                if(nums[second] + nums[third] == target){
                    ans.push_back({nums[first], nums[second], nums[third]});
                }
            }
        }
        return ans;
    }
};
```
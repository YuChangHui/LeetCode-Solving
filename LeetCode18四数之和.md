[18.四数之和](https://leetcode-cn.com/problems/4sum/)

# 题目描述

给定一个包含 n 个整数的数组 nums 和一个目标值 target，判断 nums 中是否存在四个元素 a，b，c 和 d ，使得 a + b + c + d 的值与 target 相等？找出所有满足条件且不重复的四元组。

注意：

答案中不可以包含重复的四元组。

**示例:**

```
给定数组 nums = [1, 0, -1, 0, -2, 2]，和 target = 0。

满足要求的四元组集合为：
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```

# 题解

暴力解法的时间复杂度为O(n^4^)，会超过题目时间限制。

使用排序+双层循环+双指针方法，可以将算法的时间复杂度优化为O(n^3^)。

思路与三数之和类似，注意总体思路，剪枝策略一开始可以不考虑，等到熟练以后再考虑剪枝。

# 代码

```java
//Java
//执行用时：4ms
//内存消耗：39MB
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        //定义返回值
        List<List<Integer>> result = new ArrayList<>();
        //当数组为null或者数组长度小于4，直接返回结果
        if(nums == null || nums.length < 4){
            return result;
        }
        //对数组进行排序
        Arrays.sort(nums);
        int length = nums.length;
        for(int first = 0; first < length - 3; first++){
            //当first的值与前面的值相等时忽略
            if(first > 0 && nums[first] == nums[first - 1]){
                continue;
            }
            //获取当前最小值，如果最小值比目标值大，说明后面的比较不用进行了，直接break（属于优化）
            int min1 = nums[first] + nums[first+1] + nums[first+2] + nums[first+3];
            if(min1 > target){
                break;
            }
            //获取当前最大值，如果最大值比目标值小，说明此次循环不用进行，直接continue进入下一次循环
            int max1 = nums[first] + nums[length-1] + nums[length-2] + nums[length-3];
            if(max1 < target){
                continue;
            }
            //第二层循环，初始值指向first+1
            for(int second = first + 1; second < length - 2; second++){
                //当second不是第二层循环第一个数且与前面的数相同时，跳过该次循环
                if(second > first + 1 && nums[second] == nums[second-1]){
                    continue;
                }
                //定义第三个数指向第二个数后一个数，第四个数指向数组末尾
                int third = second + 1;
                int fourth = length - 1;
                //获取当前最小值，并做剪枝判断
                int min2 = nums[first] + nums[second] + nums[third] + nums[third+1];
                if(min2 > target){
                    break;
                }
                //获取当前最大值，并做剪枝判断
                int max2 = nums[first] + nums[second] + nums[fourth] + nums[fourth-1];
                if(max2 < target){
                    continue;
                }
                while(third < fourth){
                    int curr = nums[first] + nums[second]+ nums[third]+ nums[fourth];
                    if(curr == target){
                        result.add(Arrays.asList(nums[first], nums[second], nums[third], nums[fourth]));
                        third++;
                        while(third < fourth && nums[third] == nums[third-1]){
                            third++;
                        }
                        fourth--;
                        while(third < fourth && nums[fourth] == nums[fourth+1]){
                            fourth--;
                        }
                    }else if(curr > target){
                        fourth--;
                    }else{
                        third++;
                    }
                }
            }
        }
        return result;
    }
}
```


#题目

leetcode : [三数之和](https://leetcode-cn.com/problems/3sum/)

## 排序 + 双指针
- 去重  
在同一层循环中，相邻两次枚举的元素不能相同，否则会造成循环。
- 双指针  
随着第一个元素是递增的，第二个元素是递减的时候，就可以使用双指针的方法，将两重循环，合并为一重。
```Java
    class Solution {
        public List<List<Integer>> threeSum(int[] nums) {
            Arrays.sort(nums);
            List<List<Integer>> res = new LinkedList<List<Integer>>();
            for(int i=0;i<nums.length;i++){
                if(i>0 && nums[i]==nums[i-1]){
                    continue;
                }
                int target = -nums[i];
                int left = i+1;
                int right = nums.length-1;
                while(left<right){
                    if(nums[left]+nums[right]>target){
                        right--;
                    }
                    else if(nums[left]+nums[right]<target){
                        left++;
                    }
                    else{
                        res.add(Arrays.asList(nums[i], nums[left], nums[right]));
                        while(left<right && nums[left]==nums[left+1]){
                            left++;
                        }
                        while(right>left && nums[right]==nums[right-1]){
                            right--;
                        }
                        left++;
                        right--;
                    }
                }
            }
            return res;
        }

    }

```

#Leetcode day6 26. Remove Duplicates from Sorted Array

##Description 
***
>Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

>Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

***

## Algorithm

>
Since the array is already sorted, we can keep two pointers fast and slow. As long as nums[fast] = nums[slow], we increment fast to skip the duplicate.
When we encounter nums[fast]!= nums[slow], the duplicate run ends and we increment the slow, then copy the new value to nums[slow] until we reach the end of the array.


## Two efficient C++ Approach 

```
class Solution {
public:
    int removeDuplicates(vector<int>& nums) 
    {
        
        int count = 0;
        int n = nums.size();
        for(int i = 1; i < n; i++){
            if(nums[i] == nums[i-1]) count++;
            else nums[i-count] = nums[i];
        }
        
        
        return n-count;

    }
};

```

```
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if (nums.size()==0) return 0;
        int slow = 0;
        for (int fast = 1; fast < nums.size(); ++fast)
        {
            if (nums[fast] != nums[slow])
            {
                slow ++;
                nums[slow] = nums[fast];
                
            }
        }
        return slow+1;
    }
};

```

## Python3 

```
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        #two pointers
        
        for slow in range(len(nums)):
            
            fast = slow + 1
            if fast == len(nums):
                return len(nums)
            while nums[slow] == nums[fast]:
                del nums[fast]
                
                if fast>=len(nums):
                    return len(nums)
            
        return len(nums)
   
 ```
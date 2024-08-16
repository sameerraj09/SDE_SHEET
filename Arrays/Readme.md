**1752. Check if Array Is Sorted and Rotated**
Approach:- if there will be more than one breaking point means that is not srted rotated
The initial check if (nums[0] < nums[nums.length - 1]) is used to account for cases where 
the array is either fully sorted (not rotated) or has been rotated in such a way that the last element is smaller than the first. 
It ensures that such cases don't falsely return false when they should return true.
Lets take one example 1,2,3,4 rotate once --> 2 3 4 1 
                              rotate twice-->3 4 1 2        in all case the last element is smaller than the first value and only one breaking point exist
                              rotate thrice-->4 1 2 3
```
class Solution {
    public boolean check(int[] nums) {
        int count=0;
        if (nums[0] < nums[nums.length - 1]) {     //this condition will false for the rotated sorted array bcs the first element is always greater than the last element
            count++;                             //if no rotation and all element are sorted the count will be one
        }
        for(int i=0;i<nums.length-1;i++){
            if(nums[i]>nums[i+1]){         //breking the order
                count++;
            }
            if(count>1){
                return false;  //if more than one then not a rotated sorted array
            }
        }
        return true;
    }
   
}

```
                            

**73. Set Matrix Zeroes**

Store zero positions: Traverse the matrix and save the indices of all zeros.
Set rows and columns to zero: For each saved zero, set the entire row and column to zero using a helper function.
```
class Solution {
    public void setZeroes(int[][] matrix) {
        ArrayList<int []> store = new ArrayList<>();
          int row = matrix.length;
          int col = matrix[0].length;
        for(int i =0;i<row;i++){
            for(int j = 0;j<col;j++){
             if(matrix[i][j]==0) {
                store.add(new int[]{i,j});
             }
            }
        }
        for(int [] curr: store){
            int row1 = curr[0];
            int col1 = curr[1];
            setzero(row1,col1, matrix);

        }
    }
        public void setzero(int row,int col , int matrix[][]){
            int m = matrix.length;
            int n = matrix[0].length; 
            for(int i = 0;i<m;i++){
                matrix[i][col] =0;
            }
            for(int j = 0;j<n;j++){
                matrix[row][j]=0;
            }
        }
    }

```

**118. Pascal's Triangle**

Steps to Generate Pascal's Triangle:

Initialize an empty list: 

Create an outer list ans to store all rows of the triangle.

Iterate through rows: For each row (from 0 to numRows-1):

Start a new list curr for the current row.

Add 1 as the first element of each row.

For intermediate elements (between the first and last), calculate the sum of the two numbers directly above from the previous row.

Add 1 as the last element for rows greater than 0.

Add current row: Append the curr list to the main ans list.

Return the result: Once all rows are generated, return the complete triangle.

This method builds each row based on the previous row’s values.

```
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>>  ans= new ArrayList<>();
        for(int i = 0;i<numRows;i++){
            List<Integer> curr = new ArrayList<>();
            curr.add(1);
            for(int j = 1;j<i;j++){
                int next = ans.get(i-1).get(j-1)+ans.get(i-1).get(j);
                curr.add(next);
            }
            if(i>0){
                curr.add(1);
            
            }
            ans.add(curr);
            
        }
        return ans;
    }
}
```

**31. Next Permutation**

loop reverse chalao agar nums[i+1]<nums[i] to break kar do

Find the first decreasing element from the end (right to left):

uske baad hame fir se ulta loop chalana hai aur jaise hi koi number nums[i] se bada mile usse swap karo do 

agar aisa kuch nahi mila to wo max pe hai to seedha reverse kar do wahi ans hoga

GPT:-(Simple explanation)

Explanation: 

We need to find the point from which we can increase the sequence to the next greater permutation. So, starting from the second-to-last element (nums.length - 2), we 
move leftwards until we find an element nums[i] that is smaller than its next element nums[i+1].


Reason: This nums[i] is the first element that can be swapped to create a greater permutation. If no such element is found (i.e., the entire array is in non-

increasing order), it means the array is the highest permutation possible, and the next permutation will be the smallest one (reverse the entire array).

Find the smallest number larger than nums[i] to swap:

Explanation: Once we find nums[i], we need to swap it with the smallest number that's larger than nums[i]. This ensures that the new permutation is the next lexicographically greater one.

How: Start from the last element (nums.length - 1) and move leftwards until you find an element nums[j] that is greater than nums[i].

Reverse the portion after the swapped element:

Explanation: After swapping nums[i] and nums[j], the portion of the array to the right of index i is still in non-increasing order. To get the smallest possible 
permutation, we reverse this part to make it the smallest possible sequence.

Why reverse?: Because reversing a decreasing sequence gives the smallest lexicographical order.

![image](https://github.com/user-attachments/assets/716da84f-8266-49e3-a0cf-410a02f72023)

```
class Solution {
    public void nextPermutation(int[] nums) {
        // Step 1: Find the first decreasing element from the right
        int i = nums.length - 2;
        while (i >= 0 && nums[i + 1] <= nums[i]) {
            i--;
        }

        // Step 2: If such an element is found, find the next larger element and swap
        if (i >= 0) {
            int j = nums.length - 1;
            while (nums[j] <= nums[i]) {
                j--;
            }
            swap(nums, i, j);
        }

        // Step 3: Reverse the sequence after the swapped element to get the next permutation
        reverse(nums, i + 1);
    }

    // Swap function
    public void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // Reverse function
    public void reverse(int[] arr, int i) {
        int x = i, y = arr.length - 1;
        while (x < y) {
            swap(arr, x, y);
            x++;
            y--;
        }
    }
}

```

**53. Maximum Subarray**

Approach:-

Initialize variables:

cs (current sum) starts at 0.

ans (maximum sum so far) starts at the smallest possible integer.

Traverse the array:

For each element in the array:

If cs (current sum) becomes negative, reset it to 0 (to avoid carrying a negative sum forward).

Add the current element to cs.

Update ans with the maximum of cs and ans.

Return the maximum sum (ans):
```
class Solution {
    public int maxSubArray(int[] nums) {
        int cs = 0;
        int ans = Integer.MIN_VALUE;
        for(int i = 0;i<nums.length;i++){
            if(cs<0){
                cs = 0;
            }
            cs+=nums[i];
            ans = Math.max(cs,ans);
        }
        return ans;
    }
}
```

**Sort an array of 0's, 1's and 2's**

Approach:-

Count the no of zero present in an array and no of one in array 

now start a loop till no of zeros and start filling the value 0

after that do same for 1 

```
class Solution {
    public void sortColors(int[] nums) {
         //Arrays.sort(nums);

         //fanda clear hai zero count karo ones count karo aur fir utne zero aur one array me daal do aur baki me 2 daal do
           int zero = 0;
            int ones = 0;
            for(int i = 0;i<nums.length;i++){
                if(nums[i]==0){
                    zero++;
                }
                else if(nums[i]==1){
                    ones++;
                }
                
            }
            int i = 0;
            while(zero>0){
                nums[i]=0;
                zero--;
                i++;
            }
            while(ones>0){
                nums[i]=1;
                ones--;
                i++;
            }
            while(i<nums.length){
                nums[i]=2;
                i++;
            }
    }
}
```

**Stock Buy and Sell**

Approach:-

there is simple logic if the current price of stock is less than the earlier cp then buy it 

else sell it and find profit by subtracting the value and compare that value with the max profit if it is largest update it

```
class Solution {
    public int maxProfit(int[] prices) {
        int cp = prices[0];  //pehla stock kharod lo
        int maxprofit = 0;
        for(int i=1;i<prices.length;i++){
            if(cp<prices[i]){  // aab avi wala stock mehnga hai prev wale se profit pata karo
                int profit = prices[i]-cp;
                maxprofit = Math.max(maxprofit,profit);
            }
            else{
                   cp = prices[i];   // stock sasta hai pehle wale se
            }
        }
        return maxprofit;
    }
}
```


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
                            

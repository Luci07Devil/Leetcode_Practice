# ARRAYS  
#### TWO SUM
> Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
> You may assume that each input would have exactly one solution, and you may not use the same element twice.
> You can return the answer in any order.

###### Example 1:  
    Input: nums = [2,7,11,15], target = 9  
    Output: [0,1]  
    Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].  
###### Example 2:  
    Input: nums = [3,2,4], target = 6  
    Output: [1,2]  
###### Example 3:  
    Input: nums = [3,3], target = 6  
    Output: [0,1]  
###### Constraints:
* 2 <= nums.length <= 104
* -109 <= nums[i] <= 109
* -109 <= target <= 109
* Only one valid answer exists.
###### Solution:
> ###### C++
    class Solution {
    public:
	    vector<int> twoSum(vector<int>& nums, int target) {
		    int n = nums.size();
		    unordered_map<int, int> mp; // val -> index
    
		    for (int i = 0; i < n; i++) {
			    int complement = target - nums[i];
			    if (mp.find(complement) != mp.end()) {
				    return {mp[complement], i};
			    }
			    mp.insert({nums[i], i});
		    }
		    return {};
	    }
    };  
> ###### Python
    class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        prevMap = {}  # val -> index

        for i, n in enumerate(nums):
            diff = target - n
            if diff in prevMap:
                return [prevMap[diff], i]
            prevMap[n] = i  

#### REMOVE DUPLICATES FROM SORTED ARRAY
> Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once.
> The relative order of the elements should be kept the same.
> Then return the number of unique elements in nums.
> * Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:
> * Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially.
> * The remaining elements of nums are not important as well as the size of nums. Return k.

###### Custom Judge:
> The judge will test your solution with the following code:

    int[] nums = [...]; // Input array
    int[] expectedNums = [...]; // The expected answer with correct length
    int k = removeDuplicates(nums); // Calls your implementation
    assert k == expectedNums.length;
    for (int i = 0; i < k; i++) {
    	assert nums[i] == expectedNums[i];
     }  

> If all assertions pass, then your solution will be accepted.  
###### Example 1:  
    Input: nums = [1,1,2]
    Output: 2, nums = [1,2,_]
    Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
    It does not matter what you leave beyond the returned k (hence they are underscores).
###### Example 2:  
    Input: nums = [0,0,1,1,1,2,2,3,3,4]
    Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
    Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
    It does not matter what you leave beyond the returned k (hence they are underscores). 

###### Constraints:
* 1 <= nums.length <= 3 * 104
* -100 <= nums[i] <= 100
* nums is sorted in non-decreasing order.
###### Solution:
> ###### C++
    class Solution {
    public:
    int removeDuplicates(vector<int>& nums) {
    int indx = 1;
    int numsSize = nums.size();
    for(int i = 1; i < numsSize; i++){
        if(nums[i] != nums[i-1]){
            nums[indx] = nums[i];
            indx++;
            }
        }
            return indx;
        }
    };
> ###### Python
    class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        L = 1
        
        for R in range(1, len(nums)):
            if nums[R] != nums[R - 1]:
                nums[L] = nums[R]
                L += 1
        return L  

#### REMOVE ELEMENT
> Given an integer array nums and an integer val, remove all occurrences of val in nums in-place.
> The order of the elements may be changed. Then return the number of elements in nums which are not equal to val.
> Consider the number of elements in nums which are not equal to val be k, to get accepted, you need to do the following things:
> * Change the array nums such that the first k elements of nums contain the elements which are not equal to val.
> * The remaining elements of nums are not important as well as the size of nums.
> * Return k.

###### Custom Judge:
> The judge will test your solution with the following code:

    int[] nums = [...]; // Input array
    int val = ...; // Value to remove
    int[] expectedNums = [...]; // The expected answer with correct length.
    // It is sorted with no values equaling val.
    int k = removeElement(nums, val); // Calls your implementation
    assert k == expectedNums.length;
    sort(nums, 0, k); // Sort the first k elements of nums
    for (int i = 0; i < actualLength; i++) {
    assert nums[i] == expectedNums[i];
    }
> If all assertions pass, then your solution will be accepted.  
###### Example 1:  
    Input: nums = [1,1,2]
    Output: 2, nums = [1,2,_]
    Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
    It does not matter what you leave beyond the returned k (hence they are underscores).
###### Example 2:  
    Input: nums = [0,0,1,1,1,2,2,3,3,4]
    Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
    Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
    It does not matter what you leave beyond the returned k (hence they are underscores). 

###### Constraints:
* 1 <= nums.length <= 3 * 104
* -100 <= nums[i] <= 100
* nums is sorted in non-decreasing order.

###### Solution:  
> ###### C++
    class Solution {
    public:
    int removeDuplicates(vector<int>& nums) {
    int indx = 1;
    int numsSize = nums.size();
    for(int i = 1; i < numsSize; i++){
        if(nums[i] != nums[i-1]){
            nums[indx] = nums[i];
            indx++;
            }
        }
            return indx;
        }
    };
> ###### Python
    class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        k = 0
        for i in range(len(nums)):
            if nums[i] != val:
                nums[k] = nums[i]
                k += 1
        return k  

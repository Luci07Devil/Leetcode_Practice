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

#### Plus One (Number Array -> Integer => Increment Integer => Number Array (OP))
> You are given a large integer represented as an integer array digits, where each digits[i] is the ith digit of the integer.
> The digits are ordered from most significant to least significant in left-to-right order.
> The large integer does not contain any leading 0's.
> Increment the large integer by one and return the resulting array of digits.

###### Example 1:  
    Input: digits = [1,2,3]
    Output: [1,2,4]
    Explanation: The array represents the integer 123.
    Incrementing by one gives 123 + 1 = 124.
    Thus, the result should be [1,2,4].
###### Example 2:  
    Input: digits = [4,3,2,1]
    Output: [4,3,2,2]
    Explanation: The array represents the integer 4321.
    Incrementing by one gives 4321 + 1 = 4322.
    Thus, the result should be [4,3,2,2].
###### Example 3:  
    Input: digits = [9]
    Output: [1,0]
    Explanation: The array represents the integer 9.
    Incrementing by one gives 9 + 1 = 10.
    Thus, the result should be [1,0].

###### Constraints:
* 1 <= digits.length <= 100
* 0 <= digits[i] <= 9
* digits does not contain any leading 0's.

###### Solution:  
> ###### C++
    class Solution {
    public:
    vector<int> plusOne(vector<int>& digits) {
        for (int i = digits.size() - 1; i >= 0; i--) {
            if (digits[i] < 9) {
                digits[i]++;
                return digits;
            }
            digits[i] = 0;
        }
        
        digits[0] = 1;
        digits.push_back(0);
        return digits;
	}
    };  

> ###### Python
    class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:

        for i in range(len(digits)-1, -1, -1):
            if digits[i] == 9:
                digits[i] = 0
            else:
                digits[i] = digits[i] + 1
                return digits
        return [1] + digits  

#### BINARY SEARCH
> Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums.
> If target exists, then return its index. Otherwise, return -1.
> You must write an algorithm with O(log n) runtime complexity.

###### Example 1:  
    Input: nums = [-1,0,3,5,9,12], target = 9
    Output: 4
    Explanation: 9 exists in nums and its index is 4
###### Example 2:  
    Input: nums = [-1,0,3,5,9,12], target = 2
    Output: -1
    Explanation: 2 does not exist in nums so return -1

###### Constraints:
* 1 <= nums.length <= 104
* -104 < nums[i], target < 104
* All the integers in nums are unique.
* nums is sorted in ascending order.

###### Solution:  
> ###### C++
    class Solution {
    public:
    int search(vector<int>& nums, int target) {
    int n = nums.size(); //size of the array
    int low = 0, high = n - 1;

    // Perform the steps:
    while (low <= high) {
        int mid = (low + high) / 2;
        if (nums[mid] == target) return mid;
        else if (target > nums[mid]) low = mid + 1;
        else high = mid - 1;
    }
    return -1;
    }
};  

> ###### Python
    class Solution:
    def search(self, nums: List[int], target: int) -> int:
        low, high = 0, len(nums)
        while low<=high:
            mid = low + ((high - low) // 2)
            if target > nums[mid]:
                low = mid + 1
            elif nums[mid] > target:
                high = mid - 1
            else:
                return mid
        return -1  

#### SEARCH INSERT POSITION (BINARY SEARCH)
> Given a sorted array of distinct integers and a target value, return the index if the target is found.
> If not, return the index where it would be if it were inserted in order.
> You must write an algorithm with O(log n) runtime complexity.

###### Example 1:  
    Input: nums = [1,3,5,6], target = 5
    Output: 2
###### Example 2:  
    Input: nums = [1,3,5,6], target = 2
    Output: 1
###### Example 3:  
    Input: nums = [1,3,5,6], target = 7
    Output: 4

###### Constraints:
* 1 <= nums.length <= 104
* -104 <= nums[i] <= 104
* nums contains distinct values sorted in ascending order.
* -104 <= target <= 104

###### Solution:  
> ###### C++
    class Solution {
    public:
    int searchInsert(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size() - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (nums[mid] < target)
                left = mid + 1;
            else
                right = mid - 1;
        }
        return left;
	}
    };  

> ###### Python
    class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        low, high = 0, len(nums)
        while low<high:
            mid = low +(high - low) // 2
            if target > nums[mid]:
                low = mid + 1
            else:
                high = mid
        return low

#### FLOOR IN SORTED ARRAY (BINARY SEARCH)
> Given a sorted array arr[] of size N without duplicates, and given a value x.
> Floor of x is defined as the largest element K in arr[] such that K is smaller than or equal to x.
> Find the index of K(0-based indexing).

###### Example 1:  
    Input: N = 7, x = 0, arr[] = {1,2,8,10,11,12,19}
    Output: -1
    Explanation: No element less than 0 is found. So output is "-1".
###### Example 2:  
    Input: N = 7, x = 5, arr[] = {1,2,8,10,11,12,19}
    Output: 1
###### Example 3:  
    Input: nums = [1,3,5,6], target = 7
    Output: 4
    Explanation: Largest Number less than 5 is 2 (i.e K = 2), whose index is 1(0-based indexing).

###### Constraints:
* 1 ≤ N ≤ 107
* 1 ≤ arr[i] ≤ 1018
* 0 ≤ X ≤ arr[n-1]
* Expected Time Complexity: O(log N).
* Expected Auxiliary Space: O(1).

###### Solution:  
> ###### C++
    class Solution{
    public:
    // Function to find floor of x
    // n: size of vector
    // x: element whose floor is to find
    int findFloor(vector<long long> v, long long n, long long x){
        int res=-1; // Initialize with -1 assuming no floor found
        int start=0;
        int end= n-1;
        while(start<=end)
        {
            int mid= start+ (end-start)/2;
            if(v[mid]==x)  // If current ele is equal to x, then it is the floor of x
            {
                return mid;
		}
            else if(v[mid]< x)  //If curr ele is less than x, update floorIndex & search ri8 half
            {
                res=mid;  //coz that is the present greatest smaller of x
                start= mid+1;
		}
            else  // If current ele is greater than x, search left half
	    {
                end=mid-1;
		}
	    }
        return res;
	}
    };  

> ###### Python
    class Solution:
        def findFloor(self,A,N,X):
            ans = -1
            low,high=0, N-1
            while low <= high:
                mid =(low+high)//2
                if A[mid] == X:
                    return mid
                elif A[mid] <= X:
                    ans = mid
                    low = mid +1
                else:
                    high = mid -1
            return ans


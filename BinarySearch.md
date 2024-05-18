# BINARY SEARCH
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

#### FLOOR IN SORTED ARRAY (BINARY SEARCH) (UPPER BOUND)
> Given a sorted array arr[] of size N without duplicates, and given a value x.
> Floor of x is defined as the largest element K in arr[] such that K is smaller than or equal to x.
> Find the index of K(0-based indexing).

###### KEY NOTE
* The upper bound algorithm finds the first or the smallest index in a sorted array where the value at that index is greater than the given key i.e. x.
* The upper bound is the smallest index, ind, where arr[ind] > x. But if any such index is not found, the upper bound algorithm returns n i.e. size of the given array. 

###### Example 1:  
    Input: N = 7, x = 0, arr[] = {1,2,8,10,11,12,19}
    Output: -1
    Explanation: No element less than 0 is found. So output is "-1".
###### Example 2:  
    Input: N = 7, x = 5, arr[] = {1,2,8,10,11,12,19}
    Output: 1

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

#### CEIL IN SORTED ARRAY (BINARY SEARCH) (LOWER BOUND)
> Given an unsorted array Arr[] of N integers and an integer X, find ceil of X in Arr[0..N-1].
> Ceil of X is the smallest element which is greater than or equal to X.
> Ceil of X doesn’t exist if X is greater than greatest element of Arr[].

###### KEY NOTES:
* The lower bound algorithm finds the first or the smallest index in a sorted array where the value at that index is greater than or equal to a given key i.e. x.
* The lower bound is the smallest index, ind, where arr[ind] >= x. But if any such index is not found, the lower bound algorithm returns n i.e. size of the given array.

###### Example 1:  
    Input: N = 8, X = 7 Arr[] = {5, 6, 8, 9, 6, 5, 5, 6}
    Output: 8
    Explanation: No element less than 0 is found. So output is "-1".
###### Example 2:  
    Input: 8, X = 10 Arr[] = {5, 6, 8, 9, 6, 5, 5, 6}
    Output: -1
    Explanation: ceil of 10 is not possible.

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
    int findCeil(vector<long long> v, long long n, long long x){
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
            else if(v[mid]>= x)  //If curr ele is less than x, update floorIndex & search ri8 half
            {
                res=mid;  //coz that is the present greatest smaller of x
                end= mid-1;
		}
            else  // If current ele is greater than x, search left half
	    {
                start=mid+1;
		}
	    }
        return res;
	}
    };  

> ###### Python
    class Solution:
        def findCeil(self,A,N,X):
            ans = -1
            low,high=0, N-1
            while low <= high:
                mid =(low+high)//2
                if A[mid] == X:
                    return mid
                elif A[mid] >= X:
                    ans = mid
                    high = mid -1
                else:
                    low = mid +1
            return ans

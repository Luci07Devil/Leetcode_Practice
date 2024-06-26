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
    ###### solution 1
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
    ###### solution 2
    class Solution:
        def searchInsert(self, nums: List[int], target: int) -> int:
	    low, high = 0, len(nums)-1
            while low<= high:
                mid = (low + high) //2
                if(target>nums[mid]):
                    low = mid +1
                else:
                    high = mid -1
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

#### CEIL THE FLOOR (BINARY SEARCH) (LOWER BOUND + UPPER BOUND)
> Given an unsorted array Arr[] of N integers and an integer X, find floor and ceiling of X in Arr[0..N-1].
> Floor of X is the largest element which is smaller than or equal to X. Floor of X doesn’t exist if X is smaller than smallest element of Arr[].
> Ceil of X is the smallest element which is greater than or equal to X. Ceil of X doesn’t exist if X is greater than greatest element of Arr[].
> Complete the function getFloorAndCeil() which takes the array of integers arr, n and x as parameters and returns a pair of integers denoting the answer.
> Return -1 if floor or ceil is not present.

###### KEY NOTES:
* The lower bound algorithm finds the first or the smallest index in a sorted array where the value at that index is greater than or equal to a given key i.e. x.
* The lower bound is the smallest index, ind, where arr[ind] >= x. But if any such index is not found, the lower bound algorithm returns n i.e. size of the given array.

###### Example 1:  
    Input: N = 8, X = 7, Arr[] = {5, 6, 8, 9, 6, 5, 5, 6}
    Output: 6 8
    Explanation: Floor of 7 is 6 and ceil of 7 is 8.
###### Example 2:  
    Input: N = 8, X = 10, Arr[] = {5, 6, 8, 9, 6, 5, 5, 6}
    Output: 9 -1
    Explanation: Floor of 10 is 9 but ceil of 10 is not possible.

###### Constraints:
* 1 ≤ N ≤ 105
* 1 ≤ Arr[i], X ≤ 106
* Expected Time Complexity: O(log N).
* Expected Auxiliary Space: O(1).

###### Solution:  
> ###### C++
    class Solution{
    public:
    // Function to find floor and ceil of x
    // n: size of vector
    // x: element whose floor is to find
    std::vector<int> getFloorAndCeil(std::vector<int>& arr, int n, int x) {
    std::sort(arr.begin(), arr.end());

    auto getFloor = & {
        int low = 0, high = n - 1;
        int ans = -1;
        while (low <= high) {
            int mid = (low + high) / 2;
            if (arr[mid] <= x) {
                ans = arr[mid];
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        return ans;
    };

    auto getCeil = & {
        int low = 0, high = n - 1;
        int ans = -1;
        while (low <= high) {
            int mid = (low + high) / 2;
            if (arr[mid] >= x) {
                ans = arr[mid];
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }
        return ans;
    };

    return {getFloor(x), getCeil(x)};
    }
    };  

> ###### Python
    class Solution:
    def getFloorAndCeil(arr, n, x):
    	# code here
    	arr.sort()
        def getFloor(arr,n,x):
            low,high = 0, n-1
	    ans = -1
            while (low<=high):
                mid = (low+high)//2
                if arr[mid] <= x:
                    ans = arr[mid]
                    low = mid + 1
                else:
                    high = mid -1
            return ans
        def getCeil(arr,n,x):
            low,high = 0, n-1
            ans = -1
            while (low<=high):
                mid = (low+high)//2
                if arr[mid] >= x:
                    ans = arr[mid]
                    high = mid -1
                else:
                    low = mid + 1
            return ans
        return([getFloor(arr,n,x),getCeil(arr,n,x)])

#### FIND THE FIRST AND LAST POSITION OF AN ELEMENT IN AN ARRAY (BINARY SEARCH) (LOWER BOUND + UPPER BOUND)
> Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value.
> If target is not found in the array, return [-1, -1].
> You must write an algorithm with O(log n) runtime complexity.

###### KEY NOTES:
* The upper bound algorithm finds the first or the smallest index in a sorted array where the value at that index is greater than the given key i.e. x.
* The upper bound is the smallest index, ind, where arr[ind] > x. But if any such index is not found, the upper bound algorithm returns n i.e. size of the given array. 
* The lower bound algorithm finds the first or the smallest index in a sorted array where the value at that index is greater than or equal to a given key i.e. x.
* The lower bound is the smallest index, ind, where arr[ind] >= x. But if any such index is not found, the lower bound algorithm returns n i.e. size of the given array.

###### Example 1:  
    Input: nums = [5,7,7,8,8,10], target = 8
    Output: [3, 4]
###### Example 2:  
    Input: nums = [5,7,7,8,8,10], target = 6
    Output: [-1, -1]
###### Example 3:  
    Input: nums = [], target = 0
    Output: [-1, -1]

###### Constraints:
* 0 <= nums.length <= 105
* -109 <= nums[i] <= 109
* nums is a non-decreasing array.
* -109 <= target <= 109

###### Solution:  
> ###### C++
    class Solution {
	public:
		std::vector<int> searchRange(std::vector<int>& nums, int target) {
			// leftBias=[true/false], if false, res is rightBiased
			auto binSearch = & -> int {
				int l = 0, r = nums.size() - 1;
				int i = -1;
				while (l <= r) {
					int m = (l + r) / 2;
					if (nums[m] < target) {
						l = m + 1;
					} else if (target < nums[m]) {
						r = m - 1;
					} else {
						i = m;
						if (leftBias) {
							r = m - 1;
						} else {
							l = m + 1;
						}
					}
				}
				return i;
			};
			return {binSearch(nums, target, true), binSearch(nums, target, false)};
		}
	};
  

> ###### Python
	class Solution:
		def searchRange(self, nums: List[int], target: int) -> List[int]:
			# leftBias=[True/False], if false, res is rightBiased
			def binSearch(nums, target, leftBias):
				l, r = 0, len(nums) - 1
				i = -1
				while l <= r:
					m = (l + r) // 2
					if nums[m] < target:
						l = m + 1
					elif target < nums[m]:
						r = m - 1
					else:
						i = m
						if leftBias:
							r = m - 1
						else:
							l = m + 1
				return i
			return [binSearch(nums, target, True), binSearch(nums, target, False)]

#### NUMBER OF OCCURANCES (BINARY SEARCH) (FIRST & LAST OCCURANCES)
> Given a sorted array Arr of size N and a number X, you need to find the number of occurrences of X in Arr.
> Complete the function count() which takes the array of integers arr, n, and x as parameters and returns an integer denoting the answer.
> If x is not present in the array (arr) then return 0.

###### KEY NOTES:
* The upper bound algorithm finds the first or the smallest index in a sorted array where the value at that index is greater than the given key i.e. x.
* The upper bound is the smallest index, ind, where arr[ind] > x. But if any such index is not found, the upper bound algorithm returns n i.e. size of the given array. 
* The lower bound algorithm finds the first or the smallest index in a sorted array where the value at that index is greater than or equal to a given key i.e. x.
* The lower bound is the smallest index, ind, where arr[ind] >= x. But if any such index is not found, the lower bound algorithm returns n i.e. size of the given array.

###### Example 1:  
    Input: N = 7, X = 2, Arr[] = {1, 1, 2, 2, 2, 2, 3}
    Output: 4
    Explanation: 2 occurs 4 times in the given array.
###### Example 2:  
    Input: N = 7, X = 4, Arr[] = {1, 1, 2, 2, 2, 2, 3}
    Output: 0
    Explanation: 4 is not present in the given array.

###### Constraints:
* 1 ≤ N ≤ 105
* 1 ≤ Arr[i] ≤ 106
* 1 ≤ X ≤ 106
* Expected Time Complexity: O(logN)
* Expected Auxiliary Space: O(1)

###### Solution:  
> ###### C++
	class Solution {
	public:
		int count(std::vector<int>& arr, int n, int x) {
			// leftBias=[true/false], if false, res is rightBiased
			auto binary_search = & -> int {
				int left = 0, right = n - 1;
				int result = -1;
				while (left <= right) {
					int mid = left + (right - left) / 2;
					if (arr[mid] == x) {
						result = mid;
						if (leftBias) {
							right = mid - 1;
						} else {
							left = mid + 1;
						}
					} else if (arr[mid] < x) {
						left = mid + 1;
					} else {
						right = mid - 1;
					}
				}
				return result;
			};
	
			int first_idx = binary_search(true);
			if (first_idx == -1) {
				return 0;
			}
			int last_idx = binary_search(false);
			return last_idx - first_idx + 1;
		}
	};

> ###### Python
	#User function Template for python3
	class Solution:
	
		def count(self,arr, n, x):
			# leftBias=[True/False], if false, res is rightBiased
			def binary_search(leftBias):
				left, right = 0, n - 1
				result = -1
				while left <= right:
					mid = left + (right - left) // 2
					if arr[mid] == x:
						result = mid
						if leftBias:
							right = mid - 1
						else:
							left = mid + 1
					elif arr[mid] < x:
						left = mid + 1
					else:
						right = mid - 1
				return result
		
			first_idx = binary_search(True)
			if first_idx == -1:
				return 0
			last_idx = binary_search(False)
		return last_idx - first_idx + 1

#### SEARCH IN SORTED ROTATED ARRAY (BINARY SEARCH) 
> There is an integer array nums sorted in ascending order (with distinct values).
> Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].
> Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.
> You must write an algorithm with O(log n) runtime complexity.

###### KEY NOTES:
* First, we identify the sorted half of the array.
* Determine if the target is located within this sorted half.
* If not, we eliminate that half from further consideration.
* Conversely, if the target does exist in the sorted half, we eliminate the other half.

###### Example 1:  
    Input: nums = [4,5,6,7,0,1,2], target = 0
    Output: 4
###### Example 2:  
    Input: nums = [4,5,6,7,0,1,2], target = 3
    Output: -1
###### Example 3:  
    Input: nums = [1], target = 0
    Output: -1

###### Constraints:
* 1 <= nums.length <= 5000
* -104 <= nums[i] <= 104
* All values of nums are unique.
* nums is an ascending array that is possibly rotated.
* -104 <= target <= 104

###### Solution:  
> ###### C++
	class Solution {
	public:
		int search(std::vector<int>& nums, int target) {
			int low = 0, high = nums.size() - 1;
			int ans = -1;
			while (low <= high) {
				int mid = (low + high) / 2;
				if (nums[mid] == target) {
					return mid;
				} else if (nums[low] <= nums[mid]) {
					if (nums[low] <= target && target <= nums[mid]) {
						high = mid - 1;
					} else {
						low = mid + 1;
					}
				} else {
					if (nums[mid] <= target && target <= nums[high]) {
						low = mid + 1;
					} else {
						high = mid - 1;
					}
				}
			}
			return -1;
		}
	};

> ###### Python
	class Solution:
		def search(self, nums: List[int], target: int) -> int:
			low, high = 0 , len(nums) -1
			ans = -1
			while low<=high:
				mid = (low + high )//2
				if nums[mid] == target:
					return mid
				elif nums[low] <= nums[mid]:
					if nums[low]<=target and target <= nums[mid]:
						high = mid -1
					else:
						low = mid +1
				else:
					if nums[mid]<= target and target <= nums[high]:
						low = mid +1
					else:
						high = mid -1
			return -1

#### SEARCH IN SORTED ROTATED ARRAY (BINARY SEARCH) 
> There is an integer array nums sorted in non-decreasing order (not necessarily with distinct values).
> Before being passed to your function, nums is rotated at an unknown pivot index k (0 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,4,4,5,6,6,7] might be rotated at pivot index 5 and become [4,5,6,6,7,0,1,2,4,4].
> Given the array nums after the rotation and an integer target, return true if target is in nums, or false if it is not in nums.
> You must decrease the overall operation steps as much as possible.

###### KEY NOTES:
* First, we identify the sorted half of the array.
* Determine if the target is located within this sorted half.
* If not, we eliminate that half from further consideration.
* Conversely, if the target does exist in the sorted half, we eliminate the other half.
* To handle duplicates, check if low = mid = high, if True low +1 else high -1

###### Example 1:  
    Input: nums = [2,5,6,0,0,1,2], target = 0
    Output: True
###### Example 2:  
    Input: nums = [2,5,6,0,0,1,2], target = 3
    Output: False

###### Constraints:
* 1 <= nums.length <= 5000
* -104 <= nums[i] <= 104
* nums is guaranteed to be rotated at some pivot.
* -104 <= target <= 104

###### Solution:  
> ###### C++
	class Solution {
	public:
		bool search(std::vector<int>& nums, int target) {
			int low = 0, high = nums.size() - 1;
			while (low <= high) {
				int mid = (low + high) / 2;
				if (nums[mid] == target) {
					return true;
				} else if (nums[low] == nums[mid] && nums[mid] == nums[high]) {
					low += 1;
					high -= 1;
					continue;
				} else if (nums[low] <= nums[mid]) {
					if (nums[low] <= target && target <= nums[mid]) {
						high = mid - 1;
					} else {
						low = mid + 1;
					}
				} else {
					if (nums[mid] <= target && target <= nums[high]) {
						low = mid + 1;
					} else {
						high = mid - 1;
					}
				}
			}
			return false;
		}
	};

> ###### Python
	class Solution:
		def search(self, nums: List[int], target: int) -> bool:
			low, high = 0, len(nums) -1
			while low <= high:
				mid = (low+high)//2
				if nums[mid] == target:
					return True
				elif nums[low] == nums[mid] and nums[mid] == nums[high]:
					low += 1
					high -= 1
					continue
				elif nums[low] <= nums[mid]:
					if nums[low] <= target and target <= nums[mid]:
						high = mid -1
					else:
						low = mid +1
				else:
					if nums[mid] <= target and target <= nums[high]:
						low = mid +1
					else:
						high = mid -1
			return False

#### FIND MINIMUM IN SORTED ROTATED ARRAY (BINARY SEARCH) 
> Suppose an array of length n sorted in ascending order is rotated between 1 and n times. For example, the array nums = [0,1,2,4,5,6,7] might become:
> [4,5,6,7,0,1,2] if it was rotated 4 times.
> [0,1,2,4,5,6,7] if it was rotated 7 times.
> Notice that rotating an array [a[0], a[1], a[2], ..., a[n-1]] 1 time results in the array [a[n-1], a[0], a[1], a[2], ..., a[n-2]].
> Given the sorted rotated array nums of unique elements, return the minimum element of this array.
> You must write an algorithm that runs in O(log n) time.

###### KEY NOTES:
* First, we identify the sorted half of the array.
* Determine if the target is located within this sorted half.
* If not, we eliminate that half from further consideration.
* Conversely, if the target does exist in the sorted half, we eliminate the other half.
* If left part is sorted: Pick the leftmost element i.e. arr[low], find min(ans, arr[low]), eliminate left half (low = mid+1).
* If right half is sorted:  Pick the leftmost element i.e. arr[mid]. find min(ans, arr[mid]), eliminate right half (high = mid-1).

###### Example 1:  
    Input: nums = [3,4,5,1,2]
    Output: 1
    Explanation: The original array was [1,2,3,4,5] rotated 3 times.
###### Example 2:  
    Input: nums = [4,5,6,7,0,1,2]
    Output: 0
    Explanation: The original array was [0,1,2,4,5,6,7] and it was rotated 4 times.
###### Example 3:  
    Input: nums = [11,13,15,17]
    Output: 11
    Explanation: The original array was [11,13,15,17] and it was rotated 4 times.

###### Constraints:
* n == nums.length
* 1 <= n <= 5000
* -5000 <= nums[i] <= 5000
* All the integers of nums are unique.
* nums is sorted and rotated between 1 and n times.

###### Solution:  
> ###### C++
	#include <vector>
	#include <algorithm>
	
	class Solution {
	public:
		int findMin(std::vector<int>& nums) {
			int low = 0;
			int high = nums.size() - 1;
			int ans = INT_MAX; // Equivalent to sys.maxsize in Python
	
			while (low <= high) {
				int mid = (low + high) / 2;
				if (nums[low] <= nums[mid]) {
					ans = std::min(ans, nums[low]);
					low = mid + 1;
				} else {
					ans = std::min(ans, nums[mid]);
					high = mid - 1;
				}
			}
	
			return ans;
		}
	};

> ###### Python
	import sys
	class Solution:
		def findMin(self, nums: List[int]) -> int:
			low, high = 0, len(nums) -1
			ans = sys.maxsize
			while low <= high:
				mid = (low + high) //2
				if nums[low]<=nums[mid]:
					ans = min(ans,nums[low])
					low = mid +1
				else:
					ans = min(ans,nums[mid])
					high = mid -1
			return ans

#### ROTATION (BINARY SEARCH) 
> Given an ascending sorted rotated array arr of distinct integers of size n.
> The array is right-rotated k times.
> Find the value of k.

###### KEY NOTES:
* The number of rotations in an array is equal to the index(0-based index) of its minimum element.
*  Check if 0th < nth, then array is rotated 0 times, min_ele = 0th element, break loop.
*  Check if low <= mid, then left half is sorted. if low < ans, update ans => arr[low] and index => low.
*  Check if mid <= ans, then left half is sorted. if low < ans, update ans => arr[low] and index => low.

*  MY LOGIC: find the rotation point (pivot) in the array. Pivot is the only element whose previous element is greater than it. If pivot, return pivot + 1 => (rotation count).

###### Example 1:  
    Input: n = 5, arr[] = {5, 1, 2, 3, 4}
    Output: 1
    Explanation: The given array is 5 1 2 3 4. The original sorted array is 1 2 3 4 5. We can see that the array was rotated 1 times to the right.
###### Example 2:  
    Input: n = 5 arr[] = {1, 2, 3, 4, 5}
    Output: 0
    Explanation: The given array is not rotated.

###### Constraints:
* n == nums.length
* 1 <= n <= 5000
* -5000 <= nums[i] <= 5000
* All the integers of nums are unique.
* nums is sorted and rotated between 1 and n times.

###### Solution:  
> ###### C++
	#include <iostream>
	#include <vector>
	class Solution{
	public:	
		int findKRotation(int arr[], int n) {
			// code here
			int left = 0;
			int right = n - 1;
			while (left < right) {
				int mid = left + (right - left) / 2;
				if (arr[mid] > arr[right]) {
					left = mid + 1;
				} else {
					right = mid;
				}
			}
			return left % n;
		}
	};

> ###### Python
	class Solution:
		def findKRotation(self,arr,  n):
			left, right = 0, len(arr) - 1
			while left < right:
				mid = (left + right) // 2
				if arr[mid] > arr[right]:
					left = mid + 1
				else:
					right = mid
			return (left % len(arr))

#### SINGLE ELEMENT IN A SORTED ARRAY (BINARY SEARCH) 
> You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once.
> Return the single element that appears only once.
> Your solution must run in O(log n) time and O(1) space.

###### KEY NOTES:
* Observation: Single element occurs at even indexes.
*  MY LOGIC: find the rotation point (pivot) in the array. Pivot is the only element whose previous element is greater than it. If pivot, return pivot + 1 => (rotation count).

###### Example 1:  
    Input: n = 5, arr[] = {5, 1, 2, 3, 4}
    Output: 1
    Explanation: The given array is 5 1 2 3 4. The original sorted array is 1 2 3 4 5. We can see that the array was rotated 1 times to the right.
###### Example 2:  
    Input: n = 5 arr[] = {1, 2, 3, 4, 5}
    Output: 0
    Explanation: The given array is not rotated.

###### Constraints:
* n == nums.length
* 1 <= n <= 5000
* -5000 <= nums[i] <= 5000
* All the integers of nums are unique.
* nums is sorted and rotated between 1 and n times.

###### Solution:  
> ###### C++
	#include <iostream>
	#include <vector>
	
	class Solution {
	public:
		int singleNonDuplicate(std::vector<int>& nums) {
			int left = 0;
			int right = nums.size() - 1;
			while (left < right) {
				int mid = left + (right - left) / 2;
				if (mid % 2 == 0) {
					if (nums[mid] == nums[mid + 1]) {
						left = mid + 2;
					} else {
						right = mid;
					}
				} else {
					if (nums[mid] == nums[mid - 1]) {
						left = mid + 1;
					} else {
						right = mid - 1;
					}
				}
			}
			return nums[left];
		}
	};

> ###### Python
	class Solution:
		def singleNonDuplicate(self, nums: List[int]) -> int:
			left, right = 0, len(nums) - 1
			while left < right:
				mid = left + (right - left) // 2
				if mid % 2 == 0:
					if nums[mid] == nums[mid + 1]:
						left = mid + 2
					else:
						right = mid
				else:
					if nums[mid] == nums[mid - 1]:
						left = mid + 1
					else:
						right = mid - 1
			return nums[left]

#### FIND PEAK ELEMENT (BINARY SEARCH) 
> A peak element is an element that is strictly greater than its neighbors.
> Given a 0-indexed integer array nums, find a peak element, and return its index. If the array contains multiple peaks, return the index to any of the peaks.
> You may imagine that nums[-1] = nums[n] = -∞. In other words, an element is always considered to be strictly greater than a neighbor that is outside the array.
> You must write an algorithm that runs in O(log n) time.

###### KEY NOTES:
* Check if the peak occurs on the descending side of mid, if so peak is on the left, then low = mid
* Check if the peak occurs on the ascending side of mid, if so peak is on the right, then high = mid +1
* low will have the peak element index

###### Example 1:  
    Input: nums = [1,2,3,1]
    Output: 2
    Explanation: 3 is a peak element and your function should return the index number 2.
###### Example 2:  
    Input: nums = [1,2,1,3,5,6,4]
    Output: 5
    Explanation: Return either index 1 where the peak is 2 or index 5 where the peak is 6.

###### Constraints:
* 1 <= nums.length <= 1000
* -231 <= nums[i] <= 231 - 1
* nums[i] != nums[i + 1] for all valid i.

###### Solution:  
> ###### C++
	class Solution {
	public:
		int findPeakElement(std::vector<int>& nums) {
			int left = 0;
			int right = nums.size() - 1;
			
			while (left < right) {
				int mid = left + (right - left) / 2;
				
				// Check if mid is a peak element
				if (nums[mid] > nums[mid + 1]) {
					right = mid;
				} else {
					left = mid + 1;
				}
			}
			
			return left;
		}
	};

> ###### Python
	class Solution:
		def findPeakElement(self, nums: List[int]) -> int:
			left, right = 0, len(nums) - 1
			while left < right:
				mid = left + (right - left) // 2

				# Check if mid is a peak element
				if nums[mid] > nums[mid + 1]:
					right = mid
				else:
					left = mid + 1

			return left

#### SQUARE ROOT OF A NUMBER (BINARY SEARCH) 
> Given an integer x, find the square root of x. If x is not a perfect square, then return floor(√x).
> complete the function floorSqrt() which takes x as the input parameter and return its square root.
> Note: Try Solving the question without using the sqrt function. The value of x>=0.

###### KEY NOTES:
* Check if the peak occurs on the descending side of mid, if so peak is on the left, then low = mid
* Check if the peak occurs on the ascending side of mid, if so peak is on the right, then high = mid +1
* low will have the peak element index

###### Example 1:  
    Input: x = 5
    Output: 2
    Explanation: Since, 5 is not a perfect square, floor of square_root of 5 is 2.
###### Example 2:  
    Input: nums = 4
    Output: 2
    Explanation: Since, 4 is a perfect square, so its square root is 2.

###### Constraints:
* 1 ≤ x ≤ 10^7
* Expected Time Complexity: O(log N)
* Expected Auxiliary Space: O(1)

###### Solution:  
> ###### C++
	class Solution {
	public:
		int floorSqrt(int x) {
			int low = 1, high = x;
			int ans = 0;
			while (low <= high) {
				int mid = low + (high - low) / 2;
				if (mid * mid <= x) {
					ans = mid;
					low = mid + 1;
				} else {
					high = mid - 1;
				}
			}
			return ans;
		}
	};

> ###### Python
	class Solution:
		def floorSqrt(self, x): 
		#Your code here
			low, high = 1, x
			ans = 0
			while low <= high:
				mid = (low+high) //2
				if (mid * mid)<=x:
					ans = mid
					low = mid +1
				else:
					high = mid -1
			return ans


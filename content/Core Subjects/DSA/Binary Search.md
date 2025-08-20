---
title: Binary Search
draft: false
tags: 
date: 19-Aug-2025
---
# BS on 1D Array
#### [704. Binary Search](https://leetcode.com/problems/binary-search/)
    
```cpp
// iterative O(logn) O(1)
int binarySearch(vector<int>& nums, int target) {
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

// recursive O(logn) O(logn)
int binarySearch(vector<int>& nums, int low, int high, int target) {
	if (low > high) return -1;

	int mid = (low + high) / 2;

	if (nums[mid] == target)
		return mid;
	else if (target > nums[mid])
		return binarySearch(nums, mid + 1, high, target);
	return binarySearch(nums, low, mid - 1, target);
}

```

```python
class Solution:
    def binary_search(self, l: int, r: int, nums: List[int], target: int) -> int:
		# recursive O(logn) O(logn)
        if l > r:
            return -1
        m = l + (r - l) // 2
        
        if nums[m] == target:
            return m
        if nums[m] < target:
            return self.binary_search(m + 1, r, nums, target)
        return self.binary_search(l, m - 1, nums, target)

    def search(self, nums: List[int], target: int) -> int:
        return self.binary_search(0, len(nums) - 1, nums, target)

	# Iterative O(logn) O(1)
	def search(self, nums: List[int], target: int) -> int:
		l, r = 0, len(nums) - 1

        while l <= r:
            # (l + r) // 2 can lead to overflow
            m = l + ((r - l) // 2)  

            if nums[m] > target:
                r = m - 1
            elif nums[m] < target:
                l = m + 1
            else:
                return m
        return -1
	
	# built-in function O(logn) O(1)O(logn) O(1)
	def search(self, nums: List[int], target: int) -> int:
		index = bisect.bisect_left(nums, target)
        return index if index < len(nums) and nums[index] == target else -1
```
    
- [Find the first or last occurrence of a given number in a sorted array](https://takeuforward.org/data-structure/last-occurrence-in-a-sorted-array/)
    
    ```cpp
    int solve(int n, int key, vector < int > & v) {
    	// brute force O(n) O(1)
      	int res = -1;
      	for (int i = n - 1; i >= 0; i--) {
        	if (v[i] == key) {
          		res = i;
          		break;
        	}
      	}
    
    	// optimal O(logn) O(1)
      	int start = 0;
      	int end = n - 1;
    
      	while (start <= end) {
    	    int mid = start + (end - start) / 2;
    	    if (v[mid] == key) {
    	      	res = mid;
    		    start = mid + 1;
    	    } else if (key < v[mid]) {
    	      	end = mid - 1;
    	    } else {
    	      	start = mid + 1;
    	    }
    	}
    	return res;
    }
    
    ```
    
- [Count occurrences of a number in a sorted array with duplicates](https://takeuforward.org/data-structure/count-occurrences-in-sorted-array/)
    
    ```cpp
    // brute force O(n) O(1)
    int count(vector<int>& arr, int n, int x) {
        int cnt = 0;
        for (int i = 0; i < n; i++) {
            if (arr[i] == x) cnt++;
        }
        return cnt;
    }
    
    // optimal O(logn) O(1)
    int firstOccurrence(vector<int> &arr, int n, int k) {
        int low = 0, high = n - 1;
        int first = -1;
    
        while (low <= high) {
            int mid = (low + high) / 2;
            if (arr[mid] == k) {
                first = mid;
                high = mid - 1; // imp
            }
            else if (arr[mid] < k) {
                low = mid + 1;
            }
            else {
                high = mid - 1;
            }
        }
        return first;
    }
    
    int lastOccurrence(vector<int> &arr, int n, int k) {
        int low = 0, high = n - 1;
        int last = -1;
    
        while (low <= high) {
            int mid = (low + high) / 2;
            if (arr[mid] == k) {
                last = mid;
                low = mid + 1; // imp
            }
            else if (arr[mid] < k) {
                low = mid + 1;
            }
            else {
                high = mid - 1;
            }
        }
        return last;
    }
    
    pair<int, int> firstAndLastPosition(vector<int>& arr, int n, int k) {
        int first = firstOccurrence(arr, n, k);
        if (first == -1) return { -1, -1};
        int last = lastOccurrence(arr, n, k);
        return {first, last};
    }
    
    ```
    
- [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
    
    ```cpp
    // brute force O(n) O(1)
    1. linear search
    
    // optimal O(logn) O(1)
    int search(vector<int>& arr, int n, int k) {
        int low = 0, high = n - 1;
        while (low <= high) {
            int mid = (low + high) / 2;
    
            //if mid points the target
            if (arr[mid] == k) return mid;
    
            //if left part is sorted:
            if (arr[low] <= arr[mid]) {
                if (arr[low] <= k && k <= arr[mid]) {
                    //element exists:
                    high = mid - 1;
                }
                else {
                    //element does not exist:
                    low = mid + 1;
                }
            }
            else { //if right part is sorted:
                if (arr[mid] <= k && k <= arr[high]) {
                    //element exists:
                    low = mid + 1;
                }
                else {
                    //element does not exist:
                    high = mid - 1;
                }
            }
        }
        return -1;
    }
    
    ```
    
- [81. Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/)
    
    ![image.png](image%2010.png)
    
    ```cpp
    // brute force O(n) O(1)
    1. linear search
    
    // binary search O(logn) O(1)
    bool searchInARotatedSortedArrayII(vector<int>&arr, int k) {
        int n = arr.size(); // size of the array.
        int low = 0, high = n - 1;
        while (low <= high) {
            int mid = (low + high) / 2;
    
            //if mid points the target
            if (arr[mid] == k) return true;
    
            //Edge case:
            if (arr[low] == arr[mid] && arr[mid] == arr[high]) {
                low = low + 1;
                high = high - 1;
                continue;
            }
    
            //if left part is sorted:
            if (arr[low] <= arr[mid]) {
                if (arr[low] <= k && k <= arr[mid]) {
                    //element exists:
                    high = mid - 1;
                }
                else {
                    //element does not exist:
                    low = mid + 1;
                }
            }
            else { //if right part is sorted:
                if (arr[mid] <= k && k <= arr[high]) {
                    //element exists:
                    low = mid + 1;
                }
                else {
                    //element does not exist:
                    high = mid - 1;
                }
            }
        }
        return false;
    }
    
    ```
    
- [153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)
    
    ```cpp
    // brute force O(n) O(1)
    1. linear search
    
    // optimal O(logn) O(1)
    int findMin(vector<int>& arr) {
        int low = 0, high = arr.size() - 1;
        int ans = INT_MAX;
        while (low <= high) {
            int mid = (low + high) / 2;
            //search space is already sorted
            //then arr[low] will always be
            //the minimum in that search space:
            if (arr[low] <= arr[high]) {
                ans = min(ans, arr[low]);
                break;
            }
    
            //if left part is sorted:
            if (arr[low] <= arr[mid]) {
                // keep the minimum:
                ans = min(ans, arr[low]);
    
                // Eliminate left half:
                low = mid + 1;
            }
            else { //if right part is sorted:
    
                // keep the minimum:
                ans = min(ans, arr[mid]);
    
                // Eliminate right half:
                high = mid - 1;
            }
        }
        return ans;
    }
    
    ```
    
- [Find out how many times has an array been rotated](https://takeuforward.org/arrays/find-out-how-many-times-the-array-has-been-rotated/)
    
    ![image.png](image%2011.png)
    
    ```cpp
    // brute force O(n) O(1)
    int findKRotation(vector<int> &arr) {
        int n = arr.size(); //size of array.
        int ans = INT_MAX, index = -1;
        for (int i = 0; i < n; i++) {
            if (arr[i] < ans) {
                ans = arr[i];
                index = i;
            }
        }
        return index;
    
    	// optimal O(logn) O(1)
    	int low = 0, high = arr.size() - 1;
        int ans = INT_MAX;
        int index = -1;
        while (low <= high) {
            int mid = (low + high) / 2;
            //search space is already sorted
            //then arr[low] will always be
            //the minimum in that search space:
            if (arr[low] <= arr[high]) {
                if (arr[low] < ans) {
                    index = low;
                    ans = arr[low];
                }
                break;
            }
    
            //if left part is sorted:
            if (arr[low] <= arr[mid]) {
                // keep the minimum:
                if (arr[low] < ans) {
                    index = low;
                    ans = arr[low];
                }
    
                // Eliminate left half:
                low = mid + 1;
            }
            else { //if right part is sorted:
    
                // keep the minimum:
                if (arr[mid] < ans) {
                    index = mid;
                    ans = arr[mid];
                }
    
                // Eliminate right half:
                high = mid - 1;
            }
        }
    }
    
    ```
    
- [540. Single Element in a Sorted Array](https://leetcode.com/problems/single-element-in-a-sorted-array/)
    
    ![image.png](image%2012.png)
    
    ```cpp
    // brute force O(n) O(1)
    int singleNonDuplicate(vector<int>& arr) {
        int n = arr.size(); //size of the array.
        if (n == 1) return arr[0];
    
        for (int i = 0; i < n; i++) {
            //Check for first index:
            if (i == 0) {
                if (arr[i] != arr[i + 1])
                    return arr[i];
            }
            //Check for last index:
            else if (i == n - 1) {
                if (arr[i] != arr[i - 1])
                    return arr[i];
            }
            else {
                if (arr[i] != arr[i - 1] && arr[i] != arr[i + 1])
                    return arr[i];
            }
        }
    
        return -1;
    
    	// brute force (xor) O(n) O(1)
    	int ans = 0;
        // XOR all the elements:
        for (int i = 0; i < n; i++) {
            ans = ans ^ arr[i];
        }
        return ans;
    
    	// optimal O(logn) O(1)
    	//Edge cases:
        if (n == 1) return arr[0];
        if (arr[0] != arr[1]) return arr[0];
        if (arr[n - 1] != arr[n - 2]) return arr[n - 1];
    
        int low = 1, high = n - 2;
        while (low <= high) {
            int mid = (low + high) / 2;
    
            //if arr[mid] is the single element:
            if (arr[mid] != arr[mid + 1] && arr[mid] != arr[mid - 1]) {
                return arr[mid];
            }
    
            //we are in the left:
            if ((mid % 2 == 1 && arr[mid] == arr[mid - 1])
                    || (mid % 2 == 0 && arr[mid] == arr[mid + 1])) {
                //eliminate the left half:
                low = mid + 1;
            }
            //we are in the right:
            else {
                //eliminate the right half:
                high = mid - 1;
            }
        }
    
        // dummy return statement:
        return -1;
    }
    
    ```
    
- [162. Find Peak Element](https://leetcode.com/problems/find-peak-element/)
    
    ![image.png](image%2013.png)
    
    ![image.png](image%2014.png)
    
    ![image.png](image%2015.png)
    
    ![image.png](image%2016.png)
    
    ![image.png](image%2017.png)
    
    ![image.png](image%2018.png)
    
    ```cpp
    // peak: arr[i-1] < arr[i] > arr[i+1]
    int findPeakElement(vector<int> &arr) {
        int n = arr.size(); //Size of array.
    
    	// brute force O(n) O(1)
        for (int i = 0; i < n; i++) {
            //Checking for the peak:
            if ((i == 0 || arr[i - 1] < arr[i])
                    && (i == n - 1 || arr[i] > arr[i + 1])) {
                return i;
            }
        }
    
    	// optimal O(logn) O(1)
    	// Edge cases:
        if (n == 1) return 0;
        if (arr[0] > arr[1]) return 0;
        if (arr[n - 1] > arr[n - 2]) return n - 1;
    
        int low = 1, high = n - 2;
        while (low <= high) {
            int mid = (low + high) / 2;
    
            //If arr[mid] is the peak:
            if (arr[mid - 1] < arr[mid] && arr[mid] > arr[mid + 1])
                return mid;
    
            // If we are in the left:
            if (arr[mid] > arr[mid - 1]) low = mid + 1;
    
            // If we are in the right:
            // Or, arr[mid] is a common point:
            else high = mid - 1;
        }
        // Dummy return statement
        return -1;
    }
    
    ```
    

## Lower Bound

- [Implement Lower Bound](https://takeuforward.org/arrays/implement-lower-bound-bs-2/)
    
    ```cpp
    int lowerBound(vector<int> arr, int n, int x) {
    	// brute force O(n) O(1)
        for (int i = 0; i < n; i++) {
            if (arr[i] >= x) {
                return i;
            }
        }
    
    	// optimal O(logn) O(1)
    	int low = 0, high = n - 1;
        int ans = n;
    
        while (low <= high) {
            int mid = (low + high) / 2;
            // maybe an answer
            if (arr[mid] >= x) {
                ans = mid;
                //look for smaller index on the left
                high = mid - 1;
            }
            else {
                low = mid + 1; // look on the right
            }
        }
        return n;
    }
    
    ```
    
- [35. Search Insert Position](https://leetcode.com/problems/search-insert-position/)
    
    ```cpp
    // O(logn) O(1)
    int searchInsert(vector<int>& arr, int x) {
        int n = arr.size();
        int low = 0, high = n - 1;
        int ans = n;
    
        while (low <= high) {
            int mid = (low + high) / 2;
            if (arr[mid] >= x) {
                ans = mid;
                high = mid - 1;
            }
            else {
                low = mid + 1;
            }
        }
        return ans;
    }
    
    ```
    
- [Floor/Ceil in Sorted Array](https://takeuforward.org/arrays/floor-and-ceil-in-sorted-array/)
    
    ```cpp
    // O(logn) O(1)
    // floor: largest no <= x
    int findFloor(int arr[], int n, int x) {
    	int low = 0, high = n - 1;
    	int ans = -1;
    
    	while (low <= high) {
    		int mid = (low + high) / 2;
    		// maybe an answer
    		if (arr[mid] <= x) {
    			ans = arr[mid];
    			//look for smaller index on the left
    			low = mid + 1;
    		}
    		else {
    			high = mid - 1; // look on the right
    		}
    	}
    	return ans;
    }
    
    // ceil: smallest no >= x
    int findCeil(int arr[], int n, int x) {
    	int low = 0, high = n - 1;
    	int ans = -1;
    
    	while (low <= high) {
    		int mid = (low + high) / 2;
    		// maybe an answer
    		if (arr[mid] >= x) {
    			ans = arr[mid];
    			//look for smaller index on the left
    			high = mid - 1;
    		}
    		else {
    			low = mid + 1; // look on the right
    		}
    	}
    	return ans;
    }
    
    pair<int, int> getFloorAndCeil(int arr[], int n, int x) {
    	int f = findFloor(arr, n, x);
    	int c = findCeil(arr, n, x);
    	return make_pair(f, c);
    }
    
    ```
    
- [34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
    
    ```cpp
    vector<int> searchRange(vector<int>& nums, int target) {
    	// brute force O(n) O(1)
    	int start = -1, end = -1;
        int n = nums.size();
        for(int i=0; i<n; i++){
        	if(nums[i] == target){
            	start = i;
                break;
            }
        }
        for(int i=n-1; i>=0; i--){
        	if(nums[i] == target){
            	end = i;
                break;
            }
        }
    	return {start, end};
    
    	// optimal O(logn) O(1)
        int start = lower_bound(nums.begin(), nums.end(), target) - nums.begin();
        int end = lower_bound(nums.begin(), nums.end(), target+1) - nums.begin() - 1;
        if(start < nums.size() && nums[start] == target)
        	return {start, end};
    
        return {-1, -1};
    }
    
    ```
    

## Upper Bound

- [Implement Upper Bound](https://takeuforward.org/arrays/implement-upper-bound/)
    
    ```cpp
    int upperBound(vector<int> &arr, int x, int n) {
    	// brute force O(n) O(1)
        for (int i = 0; i < n; i++) {
            if (arr[i] > x) {
                // upper bound found:
                return i;
            }
        }
    
    	// optimal O(logn) O(1)
    	int low = 0, high = n - 1;
        int ans = n;
    
        while (low <= high) {
            int mid = (low + high) / 2;
            // maybe an answer
            if (arr[mid] > x) {
                ans = mid;
                //look for smaller index on the left
                high = mid - 1;
            }
            else {
                low = mid + 1; // look on the right
            }
        }
    
        return n;
    }
    
    ```
    

# Binary Search on Answers

## Find min/max

- [875. Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)
    
    ```cpp
    int calculateTotalHours(vector<int> &v, int hourly) {
        int totalH = 0;
        int n = v.size();
        //find total hours:
        for (int i = 0; i < n; i++) {
            totalH += ceil((double)(v[i]) / (double)(hourly));
        }
        return totalH;
    }
    
    int minimumRateToEatBananas(vector<int> v, int h) {
        //Find the maximum number:
        int maxi = *(max_element(v.begin(), v.end()));
    
    	// brute force O(max(a[]) * n) O(1)
        //Find the minimum value of k:
        for (int i = 1; i <= maxi; i++) {
            int reqTime = calculateTotalHours(v, i);
            if (reqTime <= h) {
                return i;
            }
        }
    
        return maxi;
    
    	// optimal O(n * log(max(a[]))) O(1)
        int low = 1, high = *(max_element(v.begin(), v.end()));
    
        //apply binary search:
        while (low <= high) {
            int mid = (low + high) / 2;
            int totalH = calculateTotalHours(v, mid);
            if (totalH <= h) {
                high = mid - 1;
            }
            else {
                low = mid + 1;
            }
        }
        return low;
    }
    
    ```
    
- [1482. Minimum Number of Days to Make m Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/)
    
    ```cpp
    bool possible(vector<int> &arr, int day, int m, int k) {
        int n = arr.size(); //size of the array
        int cnt = 0;
        int noOfB = 0;
        // count the number of bouquets:
        for (int i = 0; i < n; i++) {
            if (arr[i] <= day) {
                cnt++;
            }
            else {
                noOfB += (cnt / k);
                cnt = 0;
            }
        }
        noOfB += (cnt / k);
        return noOfB >= m;
    }
    
    int roseGarden(vector<int> arr, int k, int m) {
        long long val = m * 1ll * k * 1ll;
        int n = arr.size(); //size of the array
        if (val > n) return -1; //impossible case.
        //find maximum and minimum:
        int mini = INT_MAX, maxi = INT_MIN;
        for (int i = 0; i < n; i++) {
            mini = min(mini, arr[i]);
            maxi = max(maxi, arr[i]);
        }
    
    	// brute force O((max(arr[])-min(arr[])+1) * N) O(1)
        for (int i = mini; i <= maxi; i++) {
            if (possible(arr, i, m, k))
                return i;
        }
        return -1;
    
    	// optimal O(log(max(arr[])-min(arr[])+1) * N) O(1)
        int low = mini, high = maxi;
        while (low <= high) {
            int mid = (low + high) / 2;
            if (possible(arr, mid, m, k)) {
                high = mid - 1;
            }
            else low = mid + 1;
        }
        return low;
    }
    
    ```
    
- [1283. Find the Smallest Divisor Given a Threshold](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/)
    
    ```cpp
    int sumByD(vector<int> &arr, int div) {
        int n = arr.size(); //size of array
        //Find the summation of division values:
        int sum = 0;
        for (int i = 0; i < n; i++) {
            sum += ceil((double)(arr[i]) / (double)(div));
        }
        return sum;
    }
    
    int smallestDivisor(vector<int>& arr, int limit) {
        int n = arr.size();
    	if (n > limit) return -1;
    
    	// brute force O(max(arr[])*N) O(1)
        int maxi = *max_element(arr.begin(), arr.end());
    
        for (int d = 1; d <= maxi; d++) {
            if (sumByD(arr, d) <= limit)
                return d;
        }
        return -1;
    
    	// optimal O(log(max(arr[]))*N) O(1)
        int low = 1, high = *max_element(arr.begin(), arr.end());
    
        //Apply binary search:
        while (low <= high) {
            int mid = (low + high) / 2;
            if (sumByD(arr, mid) <= limit) {
                high = mid - 1;
            }
            else {
                low = mid + 1;
            }
        }
        return low;
    }
    
    ```
    
- [1011. Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/)
    
    ```cpp
    int findDays(vector<int> &weights, int cap) {
        int days = 1; //First day.
        int load = 0;
        int n = weights.size(); //size of array.
        for (int i = 0; i < n; i++) {
            if (load + weights[i] > cap) {
                days += 1; //move to next day
                load = weights[i]; //load the weight.
            }
            else {
                //load the weight on the same day.
                load += weights[i];
            }
        }
        return days;
    }
    
    int leastWeightCapacity(vector<int> &weights, int d) {
    
    	// brute force O(N * (sum(weights[]) - max(weights[]) + 1)) O(1)
        int maxi = *max_element(weights.begin(), weights.end());
        int sum = accumulate(weights.begin(), weights.end(), 0);
    
        for (int i = maxi; i <= sum; i++) {
            if (findDays(weights, i) <= d) {
                return i;
            }
        }
        //dummy return statement:
        return -1;
    
    	// optimal O(N * log(sum(weights[]) - max(weights[]) + 1)) O(1)
    	int low = *max_element(weights.begin(), weights.end());
        int high = accumulate(weights.begin(), weights.end(), 0);
        while (low <= high) {
            int mid = (low + high) / 2;
            int numberOfDays = findDays(weights, mid);
            if (numberOfDays <= d) {
                //eliminate right half
                high = mid - 1;
            }
            else {
                //eliminate left half
                low = mid + 1;
            }
        }
        return low;
    }
    
    ```
    
- [1539. Kth Missing Positive Number](https://leetcode.com/problems/kth-missing-positive-number/)
    
    ![image.png](image%2019.png)
    
    ![image.png](image%2020.png)
    
    ![image.png](image%2021.png)
    
    ![image.png](image%2022.png)
    
    ```cpp
    int missingK(vector < int > vec, int n, int k) {
    	// brute force O(n) O(1)
    	for (int i = 0; i < n; i++) {
            if (vec[i] <= k) k++; //shifting k
            else break;
        }
        return k;
    
    	// optimal O(logn) O(1)
    	int low = 0, high = n - 1;
        while (low <= high) {
            int mid = (low + high) / 2;
            int missing = vec[mid] - (mid + 1);
            if (missing < k) {
                low = mid + 1;
            }
            else {
                high = mid - 1;
            }
        }
        return k + high + 1; // low = high + 1
    }
    
    ```
    

## Find min of max or max of min

- [Aggressive Cows](https://takeuforward.org/data-structure/aggressive-cows-detailed-solution/)
    
    ```cpp
    bool canWePlace(vector<int> &stalls, int dist, int cows) {
        int n = stalls.size(); //size of array
        int cntCows = 1; //no. of cows placed
        int last = stalls[0]; //position of last placed cow.
        for (int i = 1; i < n; i++) {
            if (stalls[i] - last >= dist) {
                cntCows++; //place next cow.
                last = stalls[i]; //update the last location.
            }
            if (cntCows >= cows) return true;
        }
        return false;
    }
    int aggressiveCows(vector<int> &stalls, int k) {
        int n = stalls.size(); //size of array
        //sort the stalls[]:
        sort(stalls.begin(), stalls.end());
    
    	// brute force O(NlogN) + O(N *(max(stalls[])-min(stalls[]))) O(1)
        int limit = stalls[n - 1] - stalls[0];
        for (int i = 1; i <= limit; i++) {
            if (canWePlace(stalls, i, k) == false) {
                return (i - 1);
            }
        }
        return limit;
    
    	// optimal O(NlogN) + O(N * log(max(stalls[])-min(stalls[]))) O(1)
        int low = 1, high = stalls[n - 1] - stalls[0];
        while (low <= high) {
            int mid = (low + high) / 2;
            if (canWePlace(stalls, mid, k) == true) {
                low = mid + 1;
            }
            else high = mid - 1;
        }
        return high;
    }
    
    ```
    
- [Book Allocation Problem](https://takeuforward.org/data-structure/allocate-minimum-number-of-pages/)
    
    ```cpp
    int countStudents(vector<int> &arr, int pages) {
        int n = arr.size(); //size of array.
        int students = 1;
        long long pagesStudent = 0;
        for (int i = 0; i < n; i++) {
            if (pagesStudent + arr[i] <= pages) {
                //add pages to current student
                pagesStudent += arr[i];
            }
            else {
                //add pages to next student
                students++;
                pagesStudent = arr[i];
            }
        }
        return students;
    }
    
    int findPages(vector<int>& arr, int n, int m) {
        //book allocation impossible:
        if (m > n) return -1;
    
        int low = *max_element(arr.begin(), arr.end());
        int high = accumulate(arr.begin(), arr.end(), 0);
    
    	// brute force O(N * (sum(arr[])-max(arr[])+1)) O(1)
        for (int pages = low; pages <= high; pages++) {
            if (countStudents(arr, pages) == m) {
                return pages;
            }
        }
    
    	// optimal O(N * log(sum(arr[])-max(arr[])+1)) O(1)
    	while (low <= high) {
            int mid = (low + high) / 2;
            int students = countStudents(arr, mid);
            if (students > m) {
                low = mid + 1;
            }
            else {
                high = mid - 1;
            }
        }
        return low;
    }
    
    ```
    
- [410. Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/)
    
    ```cpp
    int countPartitions(vector<int> &a, int maxSum) {
        int n = a.size(); //size of array.
        int partitions = 1;
        long long subarraySum = 0;
        for (int i = 0; i < n; i++) {
            if (subarraySum + a[i] <= maxSum) {
                //insert element to current subarray
                subarraySum += a[i];
            }
            else {
                //insert element to next subarray
                partitions++;
                subarraySum = a[i];
            }
        }
        return partitions;
    }
    
    int largestSubarraySumMinimized(vector<int> &a, int k) {
        int low = *max_element(a.begin(), a.end());
        int high = accumulate(a.begin(), a.end(), 0);
    
    	// brute force O(N * (sum(arr[])-max(arr[])+1)) O(1)
        for (int maxSum = low; maxSum <= high; maxSum++) {
            if (countPartitions(a, maxSum) == k)
                return maxSum;
        }
    
    	// optimal O(N * log(sum(arr[])-max(arr[])+1)) O(1)
    	while (low <= high) {
            int mid = (low + high) / 2;
            int partitions = countPartitions(a, mid);
            if (partitions > k) {
                low = mid + 1;
            }
            else {
                high = mid - 1;
            }
        }
        return low;
    }
    
    ```
    
- [Painter's partition](https://takeuforward.org/arrays/painters-partition-problem/)
    
    ```cpp
    int countPainters(vector<int> &boards, int time) {
        int n = boards.size(); //size of array.
        int painters = 1;
        long long boardsPainter = 0;
        for (int i = 0; i < n; i++) {
            if (boardsPainter + boards[i] <= time) {
                //allocate board to current painter
                boardsPainter += boards[i];
            }
            else {
                //allocate board to next painter
                painters++;
                boardsPainter = boards[i];
            }
        }
        return painters;
    }
    
    int findLargestMinDistance(vector<int> &boards, int k) {
        int low = *max_element(boards.begin(), boards.end());
        int high = accumulate(boards.begin(), boards.end(), 0);
    
    	// brute force O(N * (sum(arr[])-max(arr[])+1)) O(1)
        for (int time = low; time <= high; time++) {
            if (countPainters(boards, time) <= k) {
                return time;
            }
        }
    
    	// optimal O(N * log(sum(arr[])-max(arr[])+1)) O(1)
    	while (low <= high) {
            int mid = (low + high) / 2;
            int painters = countPainters(boards, mid);
            if (painters > k) {
                low = mid + 1;
            }
            else {
                high = mid - 1;
            }
        }
        return low;
    }
    
    ```
    
- [Minimize Max Distance to Gas Station](https://takeuforward.org/arrays/minimise-maximum-distance-between-gas-stations/)
    
    ```cpp
    // brute force O(k*n) O(n)
    long double minimiseMaxDistance(vector<int> &arr, int k) {
        int n = arr.size(); //size of array.
        vector<int> howMany(n - 1, 0);
    
        //Pick and place k gas stations:
        for (int gasStations = 1; gasStations <= k; gasStations++) {
            //Find the maximum section and insert the gas station
            long double maxSection = -1;
            int maxInd = -1;
            for (int i = 0; i < n - 1; i++) {
                long double diff = arr[i + 1] - arr[i];
                long double sectionLength = diff / (long double)(howMany[i] + 1);
                if (sectionLength > maxSection) {
                    maxSection = sectionLength;
                    maxInd = i;
                }
            }
            //insert the current gas station
            howMany[maxInd]++;
        }
    
        //Find the maximum distance i.e. the answer
        long double maxAns = -1;
        for (int i = 0; i < n - 1; i++) {
            long double diff = arr[i + 1] - arr[i];
            long double sectionLength = diff / (long double)(howMany[i] + 1);
            maxAns = max(maxAns, sectionLength);
        }
        return maxAns;
    }
    
    // better (heap) O(nlogn) O(n)
    long double minimiseMaxDistance(vector<int> &arr, int k) {
        int n = arr.size(); //size of array.
        vector<int> howMany(n - 1, 0);
        priority_queue<pair<long double, int>> pq;
    
        //insert the first n-1 elements into pq with respective distance values:
        for (int i = 0; i < n - 1; i++) {
            pq.push({arr[i + 1] - arr[i], i});
        }
    
        //Pick and place k gas stations:
        for (int gasStations = 1; gasStations <= k; gasStations++) {
            //Find the maximum section and insert the gas station:
            auto tp = pq.top();
            pq.pop();
            int secInd = tp.second;
    
            //insert the current gas station:
            howMany[secInd]++;
            long double inidiff = arr[secInd + 1] - arr[secInd];
            long double newSecLen = inidiff / (long double)(howMany[secInd] + 1);
            pq.push({newSecLen, secInd});
        }
    
        return pq.top().first;
    }
    
    // optimal O(n*log(Len)) + O(n) O(1)
    int numberOfGasStationsRequired(long double dist, vector<int> &arr) {
        int n = arr.size(); // size of the array
        int cnt = 0;
        for (int i = 1; i < n; i++) {
            int numberInBetween = ((arr[i] - arr[i - 1]) / dist);
            if ((arr[i] - arr[i - 1]) == (dist * numberInBetween)) {
                numberInBetween--;
            }
            cnt += numberInBetween;
        }
        return cnt;
    }
    
    long double minimiseMaxDistance(vector<int> &arr, int k) {
        int n = arr.size(); // size of the array
        long double low = 0;
        long double high = 0;
    
        //Find the maximum distance:
        for (int i = 0; i < n - 1; i++) {
            high = max(high, (long double)(arr[i + 1] - arr[i]));
        }
    
        //Apply Binary search:
        long double diff = 1e-6 ;
        while (high - low > diff) {
            long double mid = (low + high) / (2.0);
            int cnt = numberOfGasStationsRequired(mid, arr);
            if (cnt > k) {
                low = mid;
            }
            else {
                high = mid;
            }
        }
        return high;
    }
    
    ```
    

# BS on 2D Arrays

#### [Find the row with maximum number of 1's](https://takeuforward.org/arrays/find-the-row-with-maximum-number-of-1s/)
    
```cpp
// brute force O(n * m) O(1)
int rowWithMax1s(vector<vector<int>> &matrix, int n, int m) {
	int cnt_max = 0;
	int index = -1;

	//traverse the matrix:
	for (int i = 0; i < n; i++) {
		int cnt_ones = 0;
		for (int j = 0; j < m; j++) {
			cnt_ones += matrix[i][j];
		}
		if (cnt_ones > cnt_max) {
			cnt_max = cnt_ones;
			index = i;
		}
	}
	return index;
}

// optimal O(nlogm) O(1)
int lowerBound(vector<int> arr, int n, int x) {
	int low = 0, high = n - 1;
	int ans = n;

	while (low <= high) {
		int mid = (low + high) / 2;
		// maybe an answer
		if (arr[mid] >= x) {
			ans = mid;
			//look for smaller index on the left
			high = mid - 1;
		}
		else {
			low = mid + 1; // look on the right
		}
	}
	return ans;
}

int rowWithMax1s(vector<vector<int>> &matrix, int n, int m) {
	int cnt_max = 0;
	int index = -1;

	//traverse the rows:
	for (int i = 0; i < n; i++) {
		// get the number of 1's:
		int cnt_ones = m - lowerBound(matrix[i], m, 1);
		if (cnt_ones > cnt_max) {
			cnt_max = cnt_ones;
			index = i;
		}
	}
	return index;
}

```
    
#### [74. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)
    
![image.png](image%2023.png)

```cpp
// brute force O(n*m) O(1)
1. linear search

bool binarySearch(vector<int>& nums, int target) {
	int n = nums.size(); //size of the array
	int low = 0, high = n - 1;

	// Perform the steps:
	while (low <= high) {
		int mid = (low + high) / 2;
		if (nums[mid] == target) return true;
		else if (target > nums[mid]) low = mid + 1;
		else high = mid - 1;
	}
	return false;
}

bool searchMatrix(vector<vector<int>>& matrix, int target) {
	int n = matrix.size();
	int m = matrix[0].size();

	// better O(N + logM) O(1)
	for (int i = 0; i < n; i++) {
		if (matrix[i][0] <= target && target <= matrix[i][m - 1]) {
			return binarySearch(matrix[i], target);
		}
	}
	return false;

	// optimal O(log(NxM)) O(1)
	int low = 0, high = n * m - 1;
	while (low <= high) {
		int mid = (low + high) / 2;
		int row = mid / m, col = mid % m;
		if (matrix[row][col] == target) return true;
		else if (matrix[row][col] < target) low = mid + 1;
		else high = mid - 1;
	}
	return false;
}

```

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
		# brute force O(m∗n) O(1)
        for r in range(len(matrix)):
            for c in range(len(matrix[0])):
                if matrix[r][c] == target:
                    return True
        return False

		# Staircase Search O(m+n) O(1)
		m, n = len(matrix), len(matrix[0])
        r, c = 0, n - 1

        while r < m and c >= 0:
            if matrix[r][c] > target:
                c -= 1
            elif matrix[r][c] < target:
                r += 1
            else:
                return True
        return False
		
		# Binary Search O(log⁡m+log⁡n) (which reduces to O(log⁡(m∗n)) O(1)
		ROWS, COLS = len(matrix), len(matrix[0])

        top, bot = 0, ROWS - 1
        while top <= bot:
            row = (top + bot) // 2
            if target > matrix[row][-1]:
                top = row + 1
            elif target < matrix[row][0]:
                bot = row - 1
            else:
                break

        if not (top <= bot):
            return False
        row = (top + bot) // 2
        l, r = 0, COLS - 1
        while l <= r:
            m = (l + r) // 2
            if target > matrix[row][m]:
                l = m + 1
            elif target < matrix[row][m]:
                r = m - 1
            else:
                return True
        return False
	
		# binary search (one pass) O(log(m*n)) O(1) ignored
		ROWS, COLS = len(matrix), len(matrix[0])

        l, r = 0, ROWS * COLS - 1
        while l <= r:
            m = l + (r - l) // 2
            row, col = m // COLS, m % COLS
            if target > matrix[row][col]:
                l = m + 1
            elif target < matrix[row][col]:
                r = m - 1
            else:
                return True
        return False
```
    
#### [240. Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/)
    
```cpp
// brute force O(n*m) O(1)
1. linear search

bool binarySearch(vector<int>& nums, int target) {
	int n = nums.size(); //size of the array
	int low = 0, high = n - 1;

	// Perform the steps:
	while (low <= high) {
		int mid = (low + high) / 2;
		if (nums[mid] == target) return true;
		else if (target > nums[mid]) low = mid + 1;
		else high = mid - 1;
	}
	return false;
}

bool searchElement(vector<vector<int>>& matrix, int target) {
	int n = matrix.size();

	// better O(N*logM) O(1)
	for (int i = 0; i < n; i++) {
		bool flag =  binarySearch(matrix[i], target);
		if (flag) return true;
	}
	return false;

	// optimal O(n+m) O(1)
	int n = matrix.size();
	int m = matrix[0].size();
	int row = 0, col = m - 1;

	//traverse the matrix from (0, m-1):
	while (row < n && col >= 0) {
		if (matrix[row][col] == target) return true;
		else if (matrix[row][col] < target) row++;
		else col--;
	}
	return false;
}

```

---
title: Array
draft: false
tags: 
date: 19-Aug-2025
---
# Features
- similar type elements
- int arr
    - locally: puts garbage value
    - globally: puts zeros
- Max Size:
    - locally: 10^6
    - globally: 10^7
- zero based indexing
- store elements in contiguous memory location

# Data Structure
### Static Array
```python
# Insert n into arr at the next open position.
# Length is the number of 'real' values in arr, and capacity
# capacity is the size (aka memory allocated for the fixed size array).
def insertEnd(arr, n, length, capacity):
    if length < capacity:
        arr[length] = n
        
        
# Remove from the last position in the array if the array
# is not empty (i.e. length is non-zero).
def removeEnd(arr, length):
    if length > 0:
    # Overwrite last element with some default value.
    # We would also consider the length to be decreased by 1.
    arr[length - 1] = 0
    
    
# Insert n into index i after shifting elements to the right.
# Assuming i is a valid index and arr is not full.
def insertMiddle(arr, i, n, length):
    # Shift starting from the end to i.
    for index in range(length - 1, i - 1, -1):
        arr[index + 1] = arr[index]

    # Insert at i
    arr[i] = n
    
    
# Remove value at index i before shifting elements to the left.
# Assuming i is a valid index.
def removeMiddle(arr, i, length):
    # Shift starting from i + 1 to end.
    for index in range(i + 1, length):
        arr[index - 1] = arr[index]
    # No need to 'remove' arr[i], since we already shifted
        
def printArr(arr, capacity):
    for i in range(capacity):
        print(arr[i]
```
### Dynamic Array
```python
# Python arrays are dynamic by default, but this is an example of resizing.
class Array:
    def __init__(self):
        self.capacity = 2
        self.length = 0
        self.arr = [0] * 2 # Array of capacity = 2

    # Insert n in the last position of the array
    def pushback(self, n):
        if self.length == self.capacity:
            self.resize()
            
        # insert at next empty position
        self.arr[self.length] = n
        self.length += 1

    def resize(self):
        # Create new array of double capacity
        self.capacity = 2 * self.capacity
        newArr = [0] * self.capacity 
        
        # Copy elements to newArr
        for i in range(self.length):
            newArr[i] = self.arr[i]
        self.arr = newArr
        
    # Remove the last element in the array
    def popback(self):
        if self.length > 0:
            self.length -= 1
    
    # Get value at i-th index
    def get(self, i):
        if i < self.length:
            return self.arr[i]
        # Here we would throw an out of bounds exception

    # Insert n at i-th index
    def insert(self, i, n):
        if i < self.length:
            self.arr[i] = n
            return
        # Here we would throw an out of bounds exception       

    def print(self):
        for i in range(self.length):
            print(self.arr[i])
        print()
```
# Problems
### [Linear Search](https://takeuforward.org/data-structure/linear-search-in-c/)
```cpp
// O(n) O(1)
int search(int arr[],int n,int num) {
	for(int i=0;i<n;i++) {
		if(arr[i] == num)
			return i;
	}
	return -1;
}
```

```python
# O(n) O(1)
def search(arr, n, num):
    for i in range(n):
        if arr[i] == num:
            return i
    return -1
```
### [Largest Element in Array](https://takeuforward.org/data-structure/find-the-largest-element-in-an-array/)
```cpp
// brute force: O(nlogn) O(1)
int sortArr(vector<int>& arr) {
	sort(arr.begin(),arr.end());
	return arr[arr.size()-1];
}

// better: O(n) O(1)
int findLargestElement(int arr[], int n) {
  int max = arr[0];
  for (int i = 0; i < n; i++) {
	if (max < arr[i])
	  max = arr[i];
  }
  return max;
}

```

```python
# brute force: O(nlogn) O(1)
def sortArr(arr):
    arr.sort()
    return arr[len(arr) - 1]

# better: O(n) O(1)
def findLargestElement(arr, n):
    max_element = arr[0]
    for i in range(n):
        if max_element < arr[i]:
            max_element = arr[i]
    return max_element
```
### [Second Largest Element in an Array without sorting](https://takeuforward.org/data-structure/find-second-smallest-and-second-largest-element-in-an-array/)
```cpp
// brute force O(nlogn) O(1)
sort(arr,arr+n);
return arr[n-2];

// better (Two pass) O(n) O(1)
if (n < 2) return -1;
int large=INT_MIN,second_large=INT_MIN;

for(int i=0;i<n;i++)
	large=max(large,arr[i]);

for(int i=0;i<n;i++) {
	if(arr[i]>second_large && arr[i]!=large)
		second_large=arr[i];
}
return second_large;

// optimal (One pass) O(n) O(1)
if (n < 2) return -1;
int large=INT_MIN,second_large=INT_MIN;

for(int i=0;i<n;i++) {
	if (arr[i] > large) {
		second_large = large;
		large = arr[i];
	} else if (arr[i] > second_large && arr[i] != large) {
		second_large = arr[i];
  }
}

return second_large;
```

```python
# brute force O(nlogn) O(1)
def find_second_largest_brute_force(arr, n):
    arr.sort()
    return arr[n - 2]


def find_second_largest_two_pass(arr, n):
    if n < 2:
        return -1

    large = float('-inf')
    second_large = float('-inf')

	# better (Two pass) O(n) O(1)
    for i in range(n):
        large = max(large, arr[i])

    for i in range(n):
        if arr[i] > second_large and arr[i] != large:
            second_large = arr[i]

	# optimal (One pass) O(n) O(1)
	for i in range(n):
        if arr[i] > large:
            second_large = large
            large = arr[i]
        elif arr[i] > second_large and arr[i] != large:
            second_large = arr[i]
            
    return second_large
```
### [1752. Check if Array Is Sorted and Rotated](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/)
```cpp
// O(n) O(1)
bool check(vector<int>& nums) {
	int count = 0;
	for (int i = 1; i < nums.size(); i++) {
		 if(nums[i-1] > nums[i])
			count++;
	}

	if(nums[nums.size() - 1] > nums[0])
		count++;

	return count <= 1;
}

```

```python
# O(n) O(1)
def check(nums):
    count = 0
    for i in range(1, len(nums)):
        if nums[i - 1] > nums[i]:
            count += 1
    
    if nums[len(nums) - 1] > nums[0]:
        count += 1
    
    return count <= 1
```
### [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
```cpp
// Brute Force O(nlogn) O(n)
int removeDuplicates(int arr[], int n) {
  set<int> set;
  for (int i = 0; i < n; i++)
	set.insert(arr[i]);

  return set.size();
}

// optimal O(n) O(1)
int removeDuplicates(vector<int>& nums) {
	int i=0;
  for (int j=1; j<nums.size(); j++) {
	   if (nums[i] != nums[j]) {
		nums[++i] = nums[j];
  }
  return i+1;
}
```

```python
# Brute Force O(nlogn) O(n)
def removeDuplicates_brute_force(arr, n):
    s = set()
    for i in range(n):
        s.add(arr[i])
    return len(s)

# optimal O(n) O(1)
def removeDuplicates_optimal(nums):
    if not nums:
        return 0
    
    i = 0
    for j in range(1, len(nums)):
        if nums[i] != nums[j]:
            i += 1
            nums[i] = nums[j]
    return i + 1
```
### [Left Rotate an array by one place](https://takeuforward.org/data-structure/left-rotate-the-array-by-one/)
```cpp
void solve(int arr[], int n) {
  int temp = arr[0];
  for (int i = 0; i < n - 1; i++)
	arr[i] = arr[i + 1];
  arr[n - 1] = temp;
}
```

```python
def solve(arr, n):
    temp = arr[0]
    for i in range(n - 1):
        arr[i] = arr[i + 1]
    arr[n - 1] = temp
```
### [189. Rotate Array](https://leetcode.com/problems/rotate-array/)
```cpp
// brute O(n) O(n)
void Rotatetoright(int arr[], int n, int k) {
  if (n == 0) return;
  k = k % n;
  if (k > n) return;

  int temp[k];
  for (int i = n - k; i < n; i++)
	temp[i - n + k] = arr[i];
  for (int i = n - k - 1; i >= 0; i--)
	arr[i + k] = arr[i];
  for (int i = 0; i < k; i++)
	arr[i] = temp[i];
}

// optimal O(n) O(1)
void Reverse(int arr[], int start, int end) {
  while (start <= end) {
	swap(arr[start], arr[end]);
	start++;
	end--;
  }
}

void Rotateeletoright(int arr[], int n, int k) {
  // Reverse first n-k elements
  Reverse(arr, 0, n - k - 1);
  // Reverse last k elements
  Reverse(arr, n - k, n - 1);
  // Reverse whole array
  Reverse(arr, 0, n - 1);
}

```

```python
# brute O(n) O(n)
def Rotatetoright(arr, n, k):
    if n == 0:
        return
    k = k % n
    if k > n:
        return

    temp = [0] * k
    for i in range(n - k, n):
        temp[i - n + k] = arr[i]
    for i in range(n - k - 1, -1, -1):
        arr[i + k] = arr[i]
    for i in range(k):
        arr[i] = temp[i]

# optimal O(n) O(1)
def Reverse(arr, start, end):
    while start <= end:
        arr[start], arr[end] = arr[end], arr[start]
        start += 1
        end -= 1

def Rotateeletoright(arr, n, k):
    # Reverse first n-k elements
    Reverse(arr, 0, n - k - 1)
    # Reverse last k elements
    Reverse(arr, n - k, n - 1)
    # Reverse whole array
    Reverse(arr, 0, n - 1)
```
### [283. Move Zeroes](https://leetcode.com/problems/move-zeroes/)
```cpp
// brute force O(n) O(n)
vector<int> moveZeros(int n, vector<int> a) {
	vector<int> temp;
	for (int i = 0; i < n; i++) {
		if (a[i] != 0)
			temp.push_back(a[i]);
	}

	int nz = temp.size();

	for (int i = 0; i < nz; i++)
		a[i] = temp[i];

	for (int i = nz; i < n; i++)
		a[i] = 0;

	return a;
}

// optimal (two pointer) O(n) O(1)
vector<int> moveZeros(int n, vector<int> a) {
	int j = -1;
	for (int i = 0; i < n; i++) {
		if (a[i] == 0) {
			j = i;
			break;
		}
	}

	if (j == -1) return a;

	for (int i = j + 1; i < n; i++) {
		if (a[i] != 0) {
			swap(a[i], a[j]);
			j++;
		}
	}
	return a;
}

```

```python
# brute force O(n) O(n)
def moveZeros_brute_force(n, a):
    temp = []
    for i in range(n):
        if a[i] != 0:
            temp.append(a[i])

    nz = len(temp)

    for i in range(nz):
        a[i] = temp[i]

    for i in range(nz, n):
        a[i] = 0

    return a

# optimal (two pointer) O(n) O(1)
def moveZeros_optimal(n, a):
    j = -1
    for i in range(n):
        if a[i] == 0:
            j = i
            break
    
    if j == -1:
        return a
    
    for i in range(j + 1, n):
        if a[i] != 0:
            a[i], a[j] = a[j], a[i]
            j += 1
            
    return a
```
###  [Find the Union](https://takeuforward.org/data-structure/union-of-two-sorted-arrays/)
```cpp
// map O((m+n)log(m+n)) O(m+n)
vector<int> FindUnion(int arr1[], int arr2[], int n, int m) {
  map <int, int> freq;
  vector <int> Union;
  for (int i = 0; i < n; i++)
	freq[arr1[i]]++;
  for (int i = 0; i < m; i++)
	freq[arr2[i]]++;
  for (auto & it: freq)
	Union.push_back(it.first);
  return Union;
}

// set O((m+n)log(m+n)) O(m+n)
vector<int> FindUnion(int arr1[], int arr2[], int n, int m) {
  set<int> s;
  vector<int> Union;
  for (int i = 0; i < n; i++)
	s.insert(arr1[i]);
  for (int i = 0; i < m; i++)
	s.insert(arr2[i]);
  for (auto & it: s)
	Union.push_back(it);
  return Union;
}

// two pointer O(m+n) O(m+n)
vector<int> FindUnion(int arr1[], int arr2[], int n, int m) {
  int i = 0, j = 0;
  vector<int> Union;
  while (i < n && j < m) {
	if (arr1[i] <= arr2[j]) {
	  if (Union.size() == 0 || Union.back() != arr1[i])
		Union.push_back(arr1[i]);
	  i++;
	} else {
	  if (Union.size() == 0 || Union.back() != arr2[j])
		Union.push_back(arr2[j]);
	  j++;
	}
  }

  while (i < n) {
	if (Union.back() != arr1[i])
	  Union.push_back(arr1[i]);
	i++;
  }

  while (j < m) {
	if (Union.back() != arr2[j])
	  Union.push_back(arr2[j]);
	j++;
  }
  return Union;
}

```

```python
# map O((m+n)log(m+n)) O(m+n)
def FindUnion_map(arr1, arr2, n, m):
    freq = {}
    union = []
    for i in range(n):
        freq[arr1[i]] = freq.get(arr1[i], 0) + 1
    for i in range(m):
        freq[arr2[i]] = freq.get(arr2[i], 0) + 1
    for it in freq:
        union.append(it)
    return union

# set O((m+n)log(m+n)) O(m+n)
def FindUnion_set(arr1, arr2, n, m):
    s = set()
    union = []
    for i in range(n):
        s.add(arr1[i])
    for i in range(m):
        s.add(arr2[i])
    for it in s:
        union.append(it)
    return union

# two pointer O(m+n) O(m+n)
def FindUnion_two_pointer(arr1, arr2, n, m):
    i, j = 0, 0
    union = []
    while i < n and j < m:
        if arr1[i] <= arr2[j]:
            if not union or union[-1] != arr1[i]:
                union.append(arr1[i])
            i += 1
        else:
            if not union or union[-1] != arr2[j]:
                union.append(arr2[j])
            j += 1
    
    while i < n:
        if union[-1] != arr1[i]:
            union.append(arr1[i])
        i += 1
    
    while j < m:
        if union[-1] != arr2[j]:
            union.append(arr2[j])
        j += 1
    
    return union
```
### Find the Intersection
```cpp
// brute force O(m*n) O(m)
vector<int> FindUnion(int arr1[], int arr2[], int n, int m) {
	vector<int> Intersection;
	vector<int> vis(m) = {0};

	for (int i=0; i<n; i++) {
		for (int j=0; j<m; i++) {
			if (arr1[i] == arr2[j] && vis[j] == 0) {
				Intersection.push_back(arr1[i]);
				vis[j] = 1;
				break;
			}
			if (arr2[j] > arr1[i]) break;
		}
	}
}

// optimal O(m+n) O(1)
vector<int> FindUnion(int arr1[], int arr2[], int n, int m) {
	vector<int> Intersection;

	int i=0, j=0;
	while (i < n && j < m) {
		if (arr1[i] < arr2[j]) i++;
		else if (arr2[j] < arr1[i]) j++;
		else {
			Intersection.push_back(arr1[i]);
			i++;
			j++;
		}
	}
}

```

```python
# brute force O(m*n) O(m)
def FindUnion_brute_force(arr1, arr2, n, m):
    intersection = []
    vis = [0] * m
    
    for i in range(n):
        for j in range(m):
            if arr1[i] == arr2[j] and vis[j] == 0:
                intersection.append(arr1[i])
                vis[j] = 1
                break
            if arr2[j] > arr1[i]:
                break
    
    return intersection

# optimal O(m+n) O(1)
def FindUnion_optimal(arr1, arr2, n, m):
    intersection = []
    
    i, j = 0, 0
    while i < n and j < m:
        if arr1[i] < arr2[j]:
            i += 1
        elif arr2[j] < arr1[i]:
            j += 1
        else:
            intersection.append(arr1[i])
            i += 1
            j += 1
            
    return intersection
```
### [268. Missing Number](https://leetcode.com/problems/missing-number/)
```cpp
// brute force O(n^2) O(1)
int missingNumber(vector<int>&a, int N) {
	for (int i = 1; i <= N; i++) {
		int flag = 0;
		for (int j = 0; j < N - 1; j++) {
			if (a[j] == i) {
				flag = 1;
				break;
			}
		}
		if (flag == 0) return i;
	}
	return -1;
}

// better hasing O(n) O(n)
int missingNumber(vector<int>&a, int N) {
	int hash[N + 1] = {0}; //hash array
	// storing the frequencies:
	for (int i = 0; i < N - 1; i++)
		hash[a[i]]++;
	//checking the freqencies for numbers 1 to N:
	for (int i = 1; i <= N; i++) {
		if (hash[i] == 0)
			return i;
	}
	return -1;
}

// optimal sum O(n) O(1)
int missingNumber(vector<int>&a, int N) {
	int sum = (N * (N + 1)) / 2;
	int s2 = 0;
	for (int i = 0; i < N - 1; i++)
		s2 += a[i];

	int missingNum = sum - s2;
	return missingNum;
}

// optimal xor O(n) O(1)
int missingNumber(vector<int>&a, int N) {
	int xor1 = 0, xor2 = 0;
	for (int i = 0; i < N - 1; i++) {
		xor2 = xor2 ^ a[i]; // XOR of array elements
		xor1 = xor1 ^ (i + 1); //XOR up to [1...N-1]
	}
	xor1 = xor1 ^ N; //XOR up to [1...N]

	return (xor1 ^ xor2); // the missing number
}

```

```python
# brute force O(n^2) O(1)
def missingNumber_brute_force(a, N):
    for i in range(1, N + 1):
        flag = 0
        for j in range(N - 1):
            if a[j] == i:
                flag = 1
                break
        if flag == 0:
            return i
    return -1

# better hasing O(n) O(n)
def missingNumber_hashing(a, N):
    hash_array = [0] * (N + 1)
    # storing the frequencies:
    for i in range(N - 1):
        hash_array[a[i]] += 1
    # checking the freqencies for numbers 1 to N:
    for i in range(1, N + 1):
        if hash_array[i] == 0:
            return i
    return -1

# optimal sum O(n) O(1)
def missingNumber_sum(a, N):
    sum_total = (N * (N + 1)) // 2
    s2 = 0
    for i in range(N - 1):
        s2 += a[i]
    
    missingNum = sum_total - s2
    return missingNum

# optimal xor O(n) O(1)
def missingNumber_xor(a, N):
    xor1 = 0
    xor2 = 0
    for i in range(N - 1):
        xor2 = xor2 ^ a[i]  # XOR of array elements
        xor1 = xor1 ^ (i + 1)  # XOR up to [1...N-1]
    
    xor1 = xor1 ^ N  # XOR up to [1...N]
    
    return xor1 ^ xor2  # the missing number
```
### [485. Max Consecutive Ones](https://leetcode.com/problems/max-consecutive-ones/)
```cpp
int findMaxConsecutiveOnes(vector < int > & nums) {
	int cnt = 0;
	int maxi = 0;
	for (int i = 0; i < nums.size(); i++) {
		if (nums[i] == 1) cnt++;
		else cnt = 0;
		maxi = max(maxi, cnt);
	}
	return maxi;
}

```

```python
def findMaxConsecutiveOnes(nums):
    cnt = 0
    maxi = 0
    for i in range(len(nums)):
        if nums[i] == 1:
            cnt += 1
        else:
            cnt = 0
        maxi = max(maxi, cnt)
    return maxi
```
### [136. Single Number](https://leetcode.com/problems/single-number/)
```cpp
int getSingleElement(vector<int> &arr) {
	int n = arr.size();

	// brute force O(n^2) O(1)
	for (int i = 0; i < n; i++) {
		int num = arr[i];
		int cnt = 0;

		for (int j = 0; j < n; j++) {
			if (arr[j] == num)
				cnt++;
		}

		if (cnt == 1) return num;
	}
	return -1;

	// better hashing O(n) O(maxElement)
	int maxi = arr[0];
	for (int i = 0; i < n; i++) {
		maxi = max(maxi, arr[i]);
	}

	vector<int> hash(maxi + 1, 0);
	for (int i = 0; i < n; i++) {
		hash[arr[i]]++;
	}

	for (int i = 0; i < n; i++) {
		if (hash[arr[i]] == 1)
			return arr[i];
	}

	return -1;

	// better map O(nlogm) O(m) (m = size of map)
	map<int, int> mpp;
	for (int i = 0; i < n; i++)
		mpp[arr[i]]++;

	for (auto it : mpp) {
		if (it.second == 1)
			return it.first;
	}

	// optimal O(n) O(1)
	int xorr = 0;
	for (int i = 0; i < n; i++) {
		xorr = xorr ^ arr[i];
	}
	return xorr;
}

```

```python
def getSingleElement(arr):
    n = len(arr)

    # brute force O(n^2) O(1)
    for i in range(n):
        num = arr[i]
        cnt = 0
        for j in range(n):
            if arr[j] == num:
                cnt += 1
        if cnt == 1:
            return num
    return -1

    # better hashing O(n) O(maxElement)
    maxi = arr[0]
    for i in range(n):
        maxi = max(maxi, arr[i])

    hash_array = [0] * (maxi + 1)
    for i in range(n):
        hash_array[arr[i]] += 1

    for i in range(n):
        if hash_array[arr[i]] == 1:
            return arr[i]
    return -1

    # better map O(nlogm) O(m) (m = size of map)
    mpp = {}
    for i in range(n):
        mpp[arr[i]] = mpp.get(arr[i], 0) + 1

    for key, value in mpp.items():
        if value == 1:
            return key
    return -1

    # optimal O(n) O(1)
    xorr = 0
    for i in range(n):
        xorr = xorr ^ arr[i]
    return xorr
```
### [Longest subarray with given sum K(positives)](https://takeuforward.org/data-structure/longest-subarray-with-given-sum-k/
```cpp
int getLongestSubarray(vector<int>& a, long long k) {
	int n = a.size();

	// brute force O(n^2) O(1)
	int len = 0;
	for (int i = 0; i < n; i++) {
		long long s = 0;
		for (int j = i; j < n; j++) {
			s += a[j];
			if (s == k)
				len = max(len, j - i + 1);
		}
	}
	return len;

	// better (hashing) O(nlogn) O(n)
	map<long long, int> preSumMap;
	long long sum = 0;
	int maxLen = 0;
	for (int i = 0; i < n; i++) {
		sum += a[i];
		if (sum == k) {
			maxLen = max(maxLen, i + 1);
		}

		long long rem = sum - k;

		if (preSumMap.find(rem) != preSumMap.end()) {
			int len = i - preSumMap[rem];
			maxLen = max(maxLen, len);
		}

		if (preSumMap.find(sum) == preSumMap.end())
			preSumMap[sum] = i;
	}
	return maxLen;

	// optimal (two pointer) O(n) O(1)
	int left = 0, right = 0;
	long long sum = a[0];
	int maxLen = 0;
	while (right < n) {
		while (left <= right && sum > k) {
			sum -= a[left];
			left++;
		}

		if (sum == k)
			maxLen = max(maxLen, right - left + 1);

		right++;
		if (right < n) sum += a[right];
	}
	return maxLen;
}

```

```python
def getLongestSubarray(a, k):
    n = len(a)

    # brute force O(n^2) O(1)
    len_val = 0
    for i in range(n):
        s = 0
        for j in range(i, n):
            s += a[j]
            if s == k:
                len_val = max(len_val, j - i + 1)
    return len_val

    # better (hashing) O(nlogn) O(n)
    preSumMap = {}
    sum_val = 0
    maxLen = 0
    for i in range(n):
        sum_val += a[i]
        if sum_val == k:
            maxLen = max(maxLen, i + 1)

        rem = sum_val - k

        if rem in preSumMap:
            len_val = i - preSumMap[rem]
            maxLen = max(maxLen, len_val)

        if sum_val not in preSumMap:
            preSumMap[sum_val] = i
    return maxLen

    # optimal (two pointer) O(n) O(1)
    left = 0
    right = 0
    sum_val = a[0]
    maxLen = 0
    while right < n:
        while left <= right and sum_val > k:
            sum_val -= a[left]
            left += 1

        if sum_val == k:
            maxLen = max(maxLen, right - left + 1)

        right += 1
        if right < n:
            sum_val += a[right]
    return maxLen
```
    
### [Longest subarray with sum K (Positives + Negatives)](https://takeuforward.org/arrays/longest-subarray-with-sum-k-postives-and-negatives/)
```cpp
int getLongestSubarray(vector<int>& a, int k) {
	int n = a.size();

	// brute force O(n^2) O(1)
	int len = 0;
	for (int i = 0; i < n; i++) {
		int s = 0;
		for (int j = i; j < n; j++) {
			s += a[j];
			if (s == k)
				len = max(len, j - i + 1);
		}
	}
	return len;

	// optimal (hashing) o(nlogn) On)
	map<int, int> preSumMap;
	int sum = 0;
	int maxLen = 0;
	for (int i = 0; i < n; i++) {
		sum += a[i];

		if (sum == k)
			maxLen = max(maxLen, i + 1);

		int rem = sum - k;

		if (preSumMap.find(rem) != preSumMap.end()) {
			int len = i - preSumMap[rem];
			maxLen = max(maxLen, len);
		}

		if (preSumMap.find(sum) == preSumMap.end())
			preSumMap[sum] = i;
	}

	return maxLen;
}

```

```python
def getLongestSubarray(a, k):
    n = len(a)

    # brute force O(n^2) O(1)
    len_var = 0
    for i in range(n):
        s = 0
        for j in range(i, n):
            s += a[j]
            if s == k:
                len_var = max(len_var, j - i + 1)
    return len_var

    # optimal (hashing) o(nlogn) On)
    preSumMap = {}
    sum_val = 0
    maxLen = 0
    for i in range(n):
        sum_val += a[i]

        if sum_val == k:
            maxLen = max(maxLen, i + 1)

        rem = sum_val - k

        if rem in preSumMap:
            len_val = i - preSumMap[rem]
            maxLen = max(maxLen, len_val)

        if sum_val not in preSumMap:
            preSumMap[sum_val] = i

    return maxLen
```
    
### [1. Two Sum](https://leetcode.com/problems/two-sum/)
```cpp
vector<int> twoSum(int n, vector<int> &arr, int target) {
	vector<int> ans;

	// brute force O(n^2) O(1)
	for (int i = 0; i < n; i++) {
		for (int j = i + 1; j < n; j++) {
			if (arr[i] + arr[j] == target) {
				ans.push_back(i);
				ans.push_back(j);
				return ans;
			}
		}
	}
	return { -1, -1};

	// better O(n) O(n)
	unordered_map<int, int> mpp;
	for (int i = 0; i < n; i++) {
		int num = arr[i];
		int need = target - num;
		if (mpp.find(moreNeeded) != mpp.end()) {
			return {mpp[need], i};
		}
		mpp[num] = i;
	}
	return { -1, -1};

	// optimal O(nlogn) O(1)
	sort(arr.begin(), arr.end());
	int left = 0, right = n - 1;
	while (left < right) {
		int sum = arr[left] + arr[right];
		if (sum == target) {
			return {left, right}
		}
		else if (sum < target) left++;
		else right--;
	}
	return {-1, -1};
}

```

```python
def twoSum(n, arr, target):
    # brute force O(n^2) O(1)
    for i in range(n):
        for j in range(i + 1, n):
            if arr[i] + arr[j] == target:
                return [i, j]
    return [-1, -1]

    # better O(n) O(n)
    mpp = {}
    for i in range(n):
        num = arr[i]
        need = target - num
        if need in mpp:
            return [mpp[need], i]
        mpp[num] = i
    return [-1, -1]
    
    # optimal O(nlogn) O(1)
    arr.sort()
    left, right = 0, n - 1
    while left < right:
        sum_val = arr[left] + arr[right]
        if sum_val == target:
            return [left, right]
        elif sum_val < target:
            left += 1
        else:
            right -= 1
    return [-1, -1]
```
### [75. Sort Colors](https://leetcode.com/problems/sort-colors/  
```cpp
void sortArray(vector<int>& arr, int n) {

	// brute force O(nlogn) O(1)
	sort(arr.begin(), arr.end());

	// better O(n) O(1)
	int cnt0 = 0, cnt1 = 0, cnt2 = 0;

	for (int i = 0; i < n; i++) {
		if (arr[i] == 0) cnt0++;
		else if (arr[i] == 1) cnt1++;
		else cnt2++;
	}

	for (int i = 0; i < cnt0; i++) arr[i] = 0;
	for (int i = cnt0; i < cnt0 + cnt1; i++) arr[i] = 1;
	for (int i = cnt0 + cnt1; i < n; i++) arr[i] = 2;

	// optimal O(n) O(1)
	int low = 0, mid = 0, high = n - 1; // 3 pointers

	while (mid <= high) {
		if (arr[mid] == 0) {
			swap(arr[low], arr[mid]);
			low++;
			mid++;
		}
		else if (arr[mid] == 1) {
			mid++;
		}
		else {
			swap(arr[mid], arr[high]);
			high--;
		}
	}
}

```

```python
def sortArray(arr, n):
    # brute force O(nlogn) O(1)
    arr.sort()

    # better O(n) O(1)
    cnt0 = 0
    cnt1 = 0
    cnt2 = 0
    
    for i in range(n):
        if arr[i] == 0:
            cnt0 += 1
        elif arr[i] == 1:
            cnt1 += 1
        else:
            cnt2 += 1
    
    for i in range(cnt0):
        arr[i] = 0
    for i in range(cnt0, cnt0 + cnt1):
        arr[i] = 1
    for i in range(cnt0 + cnt1, n):
        arr[i] = 2

    # optimal O(n) O(1)
    low = 0
    mid = 0
    high = n - 1

    while mid <= high:
        if arr[mid] == 0:
            arr[low], arr[mid] = arr[mid], arr[low]
            low += 1
            mid += 1
        elif arr[mid] == 1:
            mid += 1
        else:
            arr[mid], arr[high] = arr[high], arr[mid]
            high -= 1
```

### [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
```cpp
int maxProfit(vector<int> &arr) {
	int maxPro = 0;
	int n = arr.size();

	// brute force O(n^2) O(1)
	for (int i = 0; i < n; i++) {
		for (int j = i + 1; j < n; j++) {
			int sell = arr[j];
			int buy = arr[i];
			maxPro = max(maxPro, sell - buy);
		}
	}

	// optimal O(n) O(1)
	int buy = arr[0];

	for (auto sell: arr) {
		buy = min(buy, sell);
		maxPro = max(maxPro, sell - buy);
	}

	return maxPro;
}

```

```python
def maxProfit(arr):
    n = len(arr)

    # brute force O(n^2) O(1)
    maxPro = 0
    for i in range(n):
        for j in range(i + 1, n):
            buy = arr[i]
            sell = arr[j]
            maxPro = max(maxPro, sell - buy)
    return maxPro

    # optimal O(n) O(1)
    maxPro = 0
    buy = arr[0]

    for sell in arr:
        buy = min(buy, sell)
        maxPro = max(maxPro, sell - buy)

    return maxPro
```
### [2149. Rearrange Array Elements by Sign](https://leetcode.com/problems/rearrange-array-elements-by-sign/)    
```cpp
vector<int> RearrangebySign(vector<int>A, int n) {
	int n = A.size();

	// brute force O(n) O(n)
	vector<int> pos;
	vector<int> neg;

	// Segregate the array into positives and negatives.
	for(int i=0;i<n;i++) {
		if(A[i] >= 0) pos.push_back(A[i]);
		else neg.push_back(A[i]);
	}

	// Positives on even indices, negatives on odd.
	for(int i=0;i<n/2;i++) {
		A[2*i] = pos[i];
		A[2*i+1] = neg[i];
	}
	return A;

	// optimal O(n) O(n)
	vector<int> ans(n,0);
	int posIndex = 0, negIndex = 1;

	for(int i = 0;i<n;i++){
		if(A[i]<0){
			ans[negIndex] = A[i];
			negIndex+=2;
		} else {
			ans[posIndex] = A[i];
			posIndex+=2;
		}
	}
	return ans;

	// if pos and neg elments are unequal
	vector<int> pos;
	vector<int> neg;

	for(int i=0;i<n;i++) {
		if(A[i]>=00) pos.push_back(A[i]);
		else neg.push_back(A[i]);
	}

	if(pos.size() < neg.size()){
	// First, fill array alternatively till the point
	// where positives and negatives ar equal in number.
		for(int i=0;i<pos.size();i++) {
			A[2*i] = pos[i];
			A[2*i+1] = neg[i];
		}

	// Fill the remaining negatives at the end of the array.
		int index = pos.size()*2;
		for(int i = pos.size();i<neg.size();i++){
			A[index] = neg[i];
			index++;
		}
	}

	// If negatives are lesser than the positives.
	else {
	  // First, fill array alternatively till the point
	  // where positives and negatives ar equal in number.
		for(int i=0;i<neg.size();i++){
			A[2*i] = pos[i];
			A[2*i+1] = neg[i];
		}

	 // Fill the remaining positives at the end of the array.
		int index = neg.size()*2;
		for(int i = neg.size();i<pos.size();i++){
			A[index] = pos[i];
			index++;
	}

	return A;
}

```

```python
def RearrangebySign(A, n):
    # brute force O(n) O(n)
    pos = []
    neg = []
    
	# # Segregate the array into positives and negatives.
    for i in range(n):
        if A[i] >= 0:
            pos.append(A[i])
        else:
            neg.append(A[i])
    
    # # Positives on even indices, negatives on odd.
    for i in range(n // 2):
        A[2 * i] = pos[i]
        A[2 * i + 1] = neg[i]
    
    return A

    # optimal O(n) O(n)
    ans = [0] * n
    posIndex, negIndex = 0, 1
    
    for i in range(n):
        if A[i] < 0:
            ans[negIndex] = A[i]
            negIndex += 2
        else:
            ans[posIndex] = A[i]
            posIndex += 2
    
    return ans

    # if pos and neg elments are unequal
    pos = []
    neg = []

    for i in range(n):
        if A[i] >= 0:
            pos.append(A[i])
        else:
            neg.append(A[i])

    if len(pos) < len(neg):
        # First, fill array alternatively till the point
        # where positives and negatives are equal in number.
        for i in range(len(pos)):
            A[2 * i] = pos[i]
            A[2 * i + 1] = neg[i]

        # Fill the remaining negatives at the end of the array.
        index = len(pos) * 2
        for i in range(len(pos), len(neg)):
            A[index] = neg[i]
            index += 1
    # If negatives are lesser than the positives.
    else:
        # First, fill array alternatively till the point
        # where positives and negatives are equal in number.
        for i in range(len(neg)):
            A[2 * i] = pos[i]
            A[2 * i + 1] = neg[i]

        # Fill the remaining positives at the end of the array.
        index = len(neg) * 2
        for i in range(len(neg), len(pos)):
            A[index] = pos[i]
            index += 1

    return A
```
### [31. Next Permutation](https://leetcode.com/problems/next-permutation/)
```cpp
// brute force O(n! * n) O(1)
1. generate all permutation using recursion
2. do linear search
3. find next permutation

// better
next_permutation(arr,arr+3);

// optimal O(n) O(1)
vector<int> nextGreaterPermutation(vector<int> &A) {
	int n = A.size();

	// Step 1: Find the break point:
	int ind = -1; // break point
	for (int i = n - 2; i >= 0; i--) {
		if (A[i] < A[i + 1]) {
			// index i is the break point
			ind = i;
			break;
		}
	}

	// If break point does not exist:
	if (ind == -1) {
		// reverse the whole array:
		reverse(A.begin(), A.end());
		return A;
	}

	// Step 2: Find the next greater element
	//         and swap it with arr[ind]:
	for (int i = n - 1; i > ind; i--) {
		if (A[i] > A[ind]) {
			swap(A[i], A[ind]);
			break;
		}
	}

	// Step 3: reverse the right half:
	reverse(A.begin() + ind + 1, A.end());

	return A;
}

```

```python
import itertools

# brute force O(n! * n) O(1)
# 1. generate all permutation using recursion
# 2. do linear search
# 3. find next permutation

# better
arr = [1, 2, 3]
next_permutation_obj = itertools.permutations(arr)
try:
    next_perm = next(next_permutation_obj)
    print(list(next_perm))
except StopIteration:
    print("No next permutation exists.")


# optimal O(n) O(1)
def nextGreaterPermutation(A):
    n = len(A)

    # Step 1: Find the break point:
    ind = -1  # break point
    for i in range(n - 2, -1, -1):
        if A[i] < A[i + 1]:
            # index i is the break point
            ind = i
            break

    # If break point does not exist:
    if ind == -1:
        # reverse the whole array:
        A.reverse()
        return A

    # Step 2: Find the next greater element
    #           and swap it with arr[ind]:
    for i in range(n - 1, ind, -1):
        if A[i] > A[ind]:
            A[i], A[ind] = A[ind], A[i]
            break

    # Step 3: reverse the right half:
    A[ind + 1:] = reversed(A[ind + 1:])

    return A
```
    
### [Leaders in an Array problem](https://takeuforward.org/data-structure/leaders-in-an-array/)
```cpp
vector<int> printLeadersBruteForce(int arr[], int n) {
	vector<int> ans;

	// brute force O(n^2) O(n)
	for (int i = 0; i < n; i++) {
		bool leader = true;
		for (int j = i + 1; j < n; j++) {
			if (arr[j] > arr[i]) {
				leader = false;
				break;
			}
		}
		if (leader)
			ans.push_back(arr[i]);
	}

	// optimal O(n) O(n)
	// Last element of an array is always a leader,
	int max = arr[n - 1];
	ans.push_back(arr[n-1]);

	for (int i=n-2; i>=0; i--) {
		if (arr[i] > max) {
			ans.push_back(arr[i]);
			max = arr[i];
		}
	}
	return ans;
}

```

```python
def printLeadersBruteForce(arr, n):
    ans = []

    # brute force O(n^2) O(n)
    for i in range(n):
        leader = True
        for j in range(i + 1, n):
            if arr[j] > arr[i]:
                leader = False
                break
        if leader:
            ans.append(arr[i])
    return ans

    # optimal O(n) O(n)
    # Last element of an array is always a leader,
    max_val = arr[n - 1]
    ans.append(arr[n - 1])

    for i in range(n - 2, -1, -1):
        if arr[i] > max_val:
            ans.append(arr[i])
            max_val = arr[i]
    return ans
```
### [128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)
```cpp
bool linearSearch(vector<int>&a, int num) {
	int n = a.size(); //size of array
	for (int i = 0; i < n; i++) {
		if (a[i] == num)
			return true;
	}
	return false;
}

int longestSuccessiveElements(vector<int>&a) {
	int n = a.size();
	int longest = 1;
	if (n == 0) return 0;

	// brute force O(n^2) O(1)
	for (int i = 0; i < n; i++) {
		int x = a[i];
		int cnt = 1;
		while (linearSearch(a, x + 1) == true) {
			x += 1;
			cnt += 1;
		}
		longest = max(longest, cnt);
	}

	// better O(nlogn) O(1)
	sort(a.begin(), a.end());
	int lastSmaller = INT_MIN;
	int cnt = 0;
	int longest = 1;

	for (int i = 0; i < n; i++) {
		if (a[i] - 1 == lastSmaller) {
			//a[i] is next element of current sequence.
			cnt += 1;
			lastSmaller = a[i];
		} else if (a[i] != lastSmaller) {
			cnt = 1;
			lastSmaller = a[i];
		}
		longest = max(longest, cnt);
	}

	// optimal O(n) O(n)
	unordered_set<int> st;
	for (int i = 0; i < n; i++)
		st.insert(a[i]);

	for (auto num: nums) {
		if (st.find(num-1) == st.end()) {
			int length = 1;
			while (st.find(num+length) != st.end())
				length++;
			longest = max(longest, length);
		}
	}

	// optimal O(n) O(n)
	unordered_map<int, int> m;

	for (int i : nums)
		if (!m[i]) {
			m[i] = m[i - 1] + m[i + 1] + 1;
			m[i - m[i - 1]] = m[i];
			m[i + m[i + 1]] = m[i];
			longest = max(longest, m[i]);
		}
	}
	return longest;
}

```

```python
def linearSearch(a, num):
    n = len(a)  # size of array
    for i in range(n):
        if a[i] == num:
            return True
    return False

def longestSuccessiveElements(a):
    n = len(a)
    longest = 1
    if n == 0:
        return 0

    # brute force O(n^2) O(1)
    for i in range(n):
        x = a[i]
        cnt = 1
        while linearSearch(a, x + 1) == True:
            x += 1
            cnt += 1
        longest = max(longest, cnt)
    return longest

    # better O(nlogn) O(1)
    a.sort()
    lastSmaller = float('-inf')
    cnt = 0
    longest = 1
    
    for i in range(n):
        if a[i] - 1 == lastSmaller:
            # a[i] is next element of current sequence.
            cnt += 1
            lastSmaller = a[i]
        elif a[i] != lastSmaller:
            cnt = 1
            lastSmaller = a[i]
        longest = max(longest, cnt)
    return longest

    # optimal O(n) O(n)
    st = set(a)
    
    for num in st:
        if num - 1 not in st:
            length = 1
            while num + length in st:
                length += 1
            longest = max(longest, length)
    return longest
    
    # optimal O(n) O(n)
    m = {}
    longest = 0
    for i in a:
        if i not in m:
            left = m.get(i - 1, 0)
            right = m.get(i + 1, 0)
            
            length = left + right + 1
            
            m[i] = length
            m[i - left] = length
            m[i + right] = length
            
            longest = max(longest, length)
    return longest
```
### [73. Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/)
```cpp
void markRow(vector<vector<int>> &matrix, int n, int m, int i) {
	for (int j = 0; j < m; j++) {
		if (matrix[i][j] != 0) {
			matrix[i][j] = -1;
		}
	}
}

void markCol(vector<vector<int>> &matrix, int n, int m, int j) {
	for (int i = 0; i < n; i++) {
		if (matrix[i][j] != 0) {
			matrix[i][j] = -1;
		}
	}
}

vector<vector<int>> zeroMatrix(vector<vector<int>> &matrix, int n, int m) {
	// brute force O(n*m(n+m)) O(1)
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			if (matrix[i][j] == 0) {
				markRow(matrix, n, m, i);
				markCol(matrix, n, m, j);
			}
		}
	}

	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			if (matrix[i][j] == -1) {
				matrix[i][j] = 0;
			}
		}
	}

	// better O(n*m) O(n+m)
	int row[n] = {0}; // row array
	int col[m] = {0}; // col array

	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			if (matrix[i][j] == 0) {
				// mark ith index of row wih 1:
				row[i] = 1;
				// mark jth index of col wih 1:
				col[j] = 1;
			}
		}
	}

	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			if (row[i] || col[j]) {
				matrix[i][j] = 0;
			}
		}
	}

	// optimal O(n*m) O(1)
	int col0 = 1;

	// step 1: Traverse the matrix and
	// mark 1st row & col accordingly:
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			if (matrix[i][j] == 0) {
				// mark i-th row:
				matrix[i][0] = 0;

				// mark j-th column:
				if (j != 0) matrix[0][j] = 0;
				else col0 = 0;
			}
		}
	}

	// Step 2: Mark with 0 from (1,1) to (n-1, m-1):
	for (int i = 1; i < n; i++) {
		for (int j = 1; j < m; j++) {
			if (matrix[i][j] != 0) {
				// check for col & row:
				if (matrix[i][0] == 0 || matrix[0][j] == 0) {
					matrix[i][j] = 0;
				}
			}
		}
	}

	//step 3: Finally mark the 1st col & then 1st row:
	if (matrix[0][0] == 0) {
		for (int j = 0; j < m; j++) {
			matrix[0][j] = 0;
		}
	}
	if (col0 == 0) {
		for (int i = 0; i < n; i++) {
			matrix[i][0] = 0;
		}
	}

	return matrix;
}

```

```python
def markRow(matrix, n, m, i):
    for j in range(m):
        if matrix[i][j] != 0:
            matrix[i][j] = -1

def markCol(matrix, n, m, j):
    for i in range(n):
        if matrix[i][j] != 0:
            matrix[i][j] = -1

def zeroMatrix(matrix, n, m):
    # brute force O(n*m(n+m)) O(1)
    for i in range(n):
        for j in range(m):
            if matrix[i][j] == 0:
                markRow(matrix, n, m, i)
                markCol(matrix, n, m, j)

    for i in range(n):
        for j in range(m):
            if matrix[i][j] == -1:
                matrix[i][j] = 0
    return matrix

    # better O(n*m) O(n+m)
    row = [0] * n  # row array
    col = [0] * m  # col array

    for i in range(n):
        for j in range(m):
            if matrix[i][j] == 0:
                # mark ith index of row wih 1:
                row[i] = 1
                # mark jth index of col wih 1:
                col[j] = 1

    for i in range(n):
        for j in range(m):
            if row[i] or col[j]:
                matrix[i][j] = 0
    return matrix

    # optimal O(n*m) O(1)
    col0 = 1

    # step 1: Traverse the matrix and
    # mark 1st row & col accordingly:
    for i in range(n):
        for j in range(m):
            if matrix[i][j] == 0:
                # mark i-th row:
                matrix[i][0] = 0

                # mark j-th column:
                if j != 0:
                    matrix[0][j] = 0
                else:
                    col0 = 0

    # Step 2: Mark with 0 from (1,1) to (n-1, m-1):
    for i in range(1, n):
        for j in range(1, m):
            if matrix[i][j] != 0:
                # check for col & row:
                if matrix[i][0] == 0 or matrix[0][j] == 0:
                    matrix[i][j] = 0

    # step 3: Finally mark the 1st col & then 1st row:
    if matrix[0][0] == 0:
        for j in range(m):
            matrix[0][j] = 0
    if col0 == 0:
        for i in range(n):
            matrix[i][0] = 0

    return matrix
```
### [48. Rotate Image](https://leetcode.com/problems/rotate-image/)
```cpp
vector<vector<int>> rotate(vector<vector<int>>& matrix) {
	int n = matrix.size();

	// brute force O(n^2) O(n^2)
	vector<vector<int>> rotated(n, vector<int> (n, 0));

	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			rotated[j][n - i - 1] = matrix[i][j];
		}
	}
	return rotated;

	// optimal O(n^2) O(1)
	//transposing the matrix
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < i; j++) {
			swap(matrix[i][j], matrix[j][i]);
		}
	}
	//reversing each row of the matrix
	for (int i = 0; i < n; i++) {
		reverse(matrix[i].begin(), matrix[i].end());
	}
}

```

```python
def rotate(matrix):
    n = len(matrix)

    # brute force O(n^2) O(n^2)
    rotated = [[0] * n for _ in range(n)]
    for i in range(n):
        for j in range(n):
            rotated[j][n - i - 1] = matrix[i][j]
    return rotated

    # optimal O(n^2) O(1)
    # transposing the matrix
    for i in range(n):
        for j in range(i):
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
    # reversing each row of the matrix
    for i in range(n):
        matrix[i].reverse()
    
    return matrix
```
    
### [54. Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)
![image.png](content/Notes/Core%20Subjects/DSA/attachments/image.png)
```cpp
// O(m*n) O(n)
vector<int> printSpiral(vector<vector<int>> mat) {
  vector<int> ans;

  int n = mat.size(); // no. of nows
  int m = mat[0].size(); // no. of columns

  // Initialize the pointers reqd for traversal.
  int top = 0, left = 0, bottom = n - 1, right = m - 1;

  // Loop until all elements are not traversed.
  while (top <= bottom && left <= right) {

	// For moving left to right
	for (int i = left; i <= right; i++)
	  ans.push_back(mat[top][i]);

	top++;

	// For moving top to bottom.
	for (int i = top; i <= bottom; i++)
	  ans.push_back(mat[i][right]);

	right--;

	// For moving right to left.
	if (top <= bottom) {
	  for (int i = right; i >= left; i--)
	   ans.push_back(mat[bottom][i]);

	  bottom--;
	}

	// For moving bottom to top.
	if (left <= right) {
	  for (int i = bottom; i >= top; i--)
		ans.push_back(mat[i][left]);

	  left++;
	}
  }
  return ans;
}

```

```python
def printSpiral(mat):
    ans = []

    n = len(mat)  # no. of rows
    m = len(mat[0])  # no. of columns

    # Initialize the pointers reqd for traversal.
    top = 0
    left = 0
    bottom = n - 1
    right = m - 1

    # Loop until all elements are not traversed.
    while top <= bottom and left <= right:

        # For moving left to right
        for i in range(left, right + 1):
            ans.append(mat[top][i])

        top += 1

        # For moving top to bottom.
        for i in range(top, bottom + 1):
            ans.append(mat[i][right])

        right -= 1

        # For moving right to left.
        if top <= bottom:
            for i in range(right, left - 1, -1):
                ans.append(mat[bottom][i])

            bottom -= 1

        # For moving bottom to top.
        if left <= right:
            for i in range(bottom, top - 1, -1):
                ans.append(mat[i][left])

            left += 1

    return ans
```
    
### [560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)
```cpp
int findAllSubarraysWithGivenSum(vector < int > & arr, int k) {
	int n = arr.size(); // size of the given array.
	int cnt = 0; // Number of subarrays:

	// brute force O(n^2) O(1)
	for (int i = 0 ; i < n; i++) {
		int sum = 0;
		for (int j = i; j < n; j++) {
			sum += arr[j];
			if (sum == k)
				cnt++;
		}
	}

	// optimal O(nlogn) O(n)
	map mpp;
	int preSum = 0;
	mpp[0] = 1;
	for (int i = 0; i < n; i++) {
		preSum += arr[i];
		int need = preSum - k;
		cnt += mpp[need];
		mpp[preSum]++;
	}
	return cnt;
}

```

```python
def findAllSubarraysWithGivenSum(arr, k):
    n = len(arr)  # size of the given array.
    cnt = 0  # Number of subarrays:

    # brute force O(n^2) O(1)
    for i in range(n):
        sum_val = 0
        for j in range(i, n):
            sum_val += arr[j]
            if sum_val == k:
                cnt += 1
    return cnt

    # optimal O(nlogn) O(n)
    mpp = {}
    preSum = 0
    mpp[0] = 1
    for i in range(n):
        preSum += arr[i]
        need = preSum - k
        cnt += mpp.get(need, 0)
        mpp[preSum] = mpp.get(preSum, 0) + 1
    return cnt
```
### [118. Pascal's Triangle](https://leetcode.com/problems/pascals-triangle/)
![image.png](image%201.png)
    
```cpp
// brute force
1. calculate nCr with factorial (increase time complexity)
2. rest is same as below.

// better O(n^3) O(1)
// (c = col no and We are running a loop for r times, where r is c-1.)
int nCr(int n, int r) {
	long long res = 1;

	// calculating nCr:
	for (int i = 0; i < r; i++) {
		res = res * (n - i);
		res = res / (i + 1);
	}
	return (int)(res);
}

vector<vector<int>> pascalTriangle(int n) {
	vector<vector<int>> ans;

	//Store the entire pascal's triangle:
	for (int row = 1; row <= n; row++) {
		vector<int> tempLst; // temporary list
		for (int col = 1; col <= row; col++) {
			tempLst.push_back(nCr(row - 1, col - 1));
		}
		ans.push_back(tempLst);
	}
	return ans;
}

// optimal O(n^2) O(1)
vector<int> generateRow(int row) {
	long long ans = 1;
	vector<int> ansRow;
	ansRow.push_back(1); //inserting the 1st element

	//calculate the rest of the elements:
	for (int col = 1; col < row; col++) {
		ans = ans * (row - col);
		ans = ans / col;
		ansRow.push_back(ans);
	}
	return ansRow;
}

vector<vector<int>> pascalTriangle(int n) {
	vector<vector<int>> ans;

	//store the entire pascal's triangle:
	for (int row = 1; row <= n; row++) {
		ans.push_back(generateRow(row));
	}
	return ans;
}

```

```python
import math

# brute force
# 1. calculate nCr with factorial (increase time complexity)
# 2. rest is same as below.

# better O(n^3) O(1)
# (c = col no and We are running a loop for r times, where r is c-1.)
def nCr(n, r):
    res = 1
    # calculating nCr:
    for i in range(r):
        res = res * (n - i)
        res = res // (i + 1)
    return int(res)

def pascalTriangle_better(n):
    ans = []
    # Store the entire pascal's triangle:
    for row in range(1, n + 1):
        tempLst = []  # temporary list
        for col in range(1, row + 1):
            tempLst.append(nCr(row - 1, col - 1))
        ans.append(tempLst)
    return ans

# optimal O(n^2) O(1)
def generateRow(row):
    ans = 1
    ansRow = []
    ansRow.append(1)  # inserting the 1st element

    # calculate the rest of the elements:
    for col in range(1, row):
        ans = ans * (row - col)
        ans = ans // col
        ansRow.append(ans)
    return ansRow

def pascalTriangle_optimal(n):
    ans = []
    # store the entire pascal's triangle:
    for row in range(1, n + 1):
        ans.append(generateRow(row))
    return ans
```
    
### [15. 3Sum](https://leetcode.com/problems/3sum/)
```cpp
vector<vector<int>> triplet(int n, vector<int> &arr) {
	// brute force O(n^3 * log(no of unique triplets) O(2 * no. of the unique triplets)
	set<vector<int>> st;

	// check all possible triplets:
	for (int i = 0; i < n; i++) {
		for (int j = i + 1; j < n; j++) {
			for (int k = j + 1; k < n; k++) {
				if (arr[i] + arr[j] + arr[k] == 0) {
					vector<int> temp = {arr[i], arr[j], arr[k]};
					sort(temp.begin(), temp.end());
					st.insert(temp);
				}
			}
		}
	}

	//store the set elements in the answer:
	vector<vector<int>> ans(st.begin(), st.end());
	return ans;

	// better  O(n^2 * log(no of unique triplets) O(2 * no. of the unique triplets + n)
	set<vector<int>> st;

	for (int i = 0; i < n; i++) {
		set<int> hashset;
		for (int j = i + 1; j < n; j++) {
			int third = -(arr[i] + arr[j]);

			if (hashset.find(third) != hashset.end()) {
				vector<int> temp = {arr[i], arr[j], third};
				sort(temp.begin(), temp.end());
				st.insert(temp);
			}
			hashset.insert(arr[j]);
		}
	}

	//store the set in the answer:
	vector<vector<int>> ans(st.begin(), st.end());
	return ans;

	// optimal O(nlogn + n^2) O(no. of quadruplets)
	vector<vector<int>> ans;
	sort(arr.begin(), arr.end());
	for (int i = 0; i < n; i++) {
		//remove duplicates:
		if (i != 0 && arr[i] == arr[i - 1]) continue;

		//moving 2 pointers:
		int j = i + 1;
		int k = n - 1;
		while (j < k) {
			int sum = arr[i] + arr[j] + arr[k];
			if (sum < 0) j++;
			else if (sum > 0) k--;
			else {
				vector<int> temp = {arr[i], arr[j], arr[k]};
				ans.push_back(temp);
				j++;
				k--;
				//skip the duplicates:
				while (j < k && arr[j] == arr[j - 1]) j++;
				while (j < k && arr[k] == arr[k + 1]) k--;
			}
		}
	}
	return ans;
}

```

```python
def triplet(n, arr):
    # brute force O(n^3 * log(no of unique triplets) O(2 * no. of the unique triplets)
    st = set()
    
    # check all possible triplets:
    for i in range(n):
        for j in range(i + 1, n):
            for k in range(j + 1, n):
                if arr[i] + arr[j] + arr[k] == 0:
                    temp = sorted([arr[i], arr[j], arr[k]])
                    st.add(tuple(temp))
    
    # store the set elements in the answer:
    ans = [list(t) for t in st]
    return ans

    # better O(n^2 * log(no of unique triplets) O(2 * no. of the unique triplets + n)
    st = set()
    
    for i in range(n):
        hashset = set()
        for j in range(i + 1, n):
            third = -(arr[i] + arr[j])
    
            if third in hashset:
                temp = sorted([arr[i], arr[j], third])
                st.add(tuple(temp))
            hashset.add(arr[j])
    
    # store the set in the answer:
    ans = [list(t) for t in st]
    return ans

    # optimal O(nlogn + n^2) O(no. of quadruplets)
    ans = []
    arr.sort()
    for i in range(n):
        # remove duplicates:
        if i != 0 and arr[i] == arr[i - 1]:
            continue

        # moving 2 pointers:
        j = i + 1
        k = n - 1
        while j < k:
            sum_val = arr[i] + arr[j] + arr[k]
            if sum_val < 0:
                j += 1
            elif sum_val > 0:
                k -= 1
            else:
                temp = [arr[i], arr[j], arr[k]]
                ans.append(temp)
                j += 1
                k -= 1
                # skip the duplicates:
                while j < k and arr[j] == arr[j - 1]:
                    j += 1
                while j < k and arr[k] == arr[k + 1]:
                    k -= 1
    return ans
```
    
### [18. 4Sum](https://leetcode.com/problems/4sum/)
```cpp
vector<vector<int>> fourSum(vector<int>& nums, int target) {
	int n = nums.size(); //size of the array

	// brute force O(n^4) O(2 * no. of the quadruplets)
	set<vector<int>> st;

	//checking all possible quadruplets:
	for (int i = 0; i < n; i++) {
		for (int j = i + 1; j < n; j++) {
			for (int k = j + 1; k < n; k++) {
				for (int l = k + 1; l < n; l++) {
					// taking bigger data type
					// to avoid integer overflow:
					long long sum = nums[i] + nums[j];
					sum += nums[k];
					sum += nums[l];

					if (sum == target) {
						vector<int> temp = {nums[i], nums[j], nums[k], nums[l]};
						sort(temp.begin(), temp.end());
						st.insert(temp);
					}
				}
			}
		}
	}
	vector<vector<int>> ans(st.begin(), st.end());
	return ans;

	// better O(n^3logm) O(2 * no. of the quadruplets + n)
	set<vector<int>> st;

	//checking all possible quadruplets:
	for (int i = 0; i < n; i++) {
		for (int j = i + 1; j < n; j++) {
			set<long long> hashset;
			for (int k = j + 1; k < n; k++) {
				// taking bigger data type
				// to avoid integer overflow:
				long long sum = nums[i] + nums[j];
				sum += nums[k];
				long long fourth = target - sum;
				if (hashset.find(fourth) != hashset.end()) {
					vector<int> temp = {nums[i], nums[j], nums[k], (int)(fourth)};
					sort(temp.begin(), temp.end());
					st.insert(temp);
				}
				// put the kth element into the hashset:
				hashset.insert(nums[k]);
			}
		}
	}
	vector<vector<int>> ans(st.begin(), st.end());
	return ans;

	// optimal O(n^3)  O(no. of quadruplets)
	vector<vector<int>> ans;

	// sort the given array:
	sort(nums.begin(), nums.end());

	//calculating the quadruplets:
	for (int i=0; i<n; i++) {
		if (i > 0 && nums[i] == nums[i-1]) continue;
		for (int j=i+1; j<n; j++) {
			if (j > i+1 && nums[j] == nums[j-1]) continue;

			int k = j+1, l = n-1;
			while (k < l) {
				long long newTarget = (long long)target - (long long)nums[i] - (long long)nums[j];

				if (nums[k] + nums[l] < newTarget) k++;
				else if (nums[k] + nums[l] > newTarget) l--;
				else {
					vector<int> temp = {nums[i], nums[j], nums[k], nums[l]};
					ans.push_back(temp);
					k++, l--;
					while (k < l && nums[k] == nums[k-1]) k++;
					while (k < l && nums[l] == nums[l+1]) l--;
			   }
			}
		}
	}
	return ans;
}

```

```python
def fourSum(nums, target):
    n = len(nums)  # size of the array

    # brute force O(n^4) O(2 * no. of the quadruplets)
    st = set()
    
    # checking all possible quadruplets:
    for i in range(n):
        for j in range(i + 1, n):
            for k in range(j + 1, n):
                for l in range(k + 1, n):
                    # taking bigger data type
                    # to avoid integer overflow:
                    current_sum = nums[i] + nums[j] + nums[k] + nums[l]
    
                    if current_sum == target:
                        temp = sorted([nums[i], nums[j], nums[k], nums[l]])
                        st.add(tuple(temp))
    
    ans = [list(t) for t in st]
    return ans

    # better O(n^3logm) O(2 * no. of the quadruplets + n)
    st = set()
    
    # checking all possible quadruplets:
    for i in range(n):
        for j in range(i + 1, n):
            hashset = set()
            for k in range(j + 1, n):
                # taking bigger data type
                # to avoid integer overflow:
                current_sum = nums[i] + nums[j] + nums[k]
                fourth = target - current_sum
    
                if fourth in hashset:
                    temp = sorted([nums[i], nums[j], nums[k], int(fourth)])
                    st.add(tuple(temp))
    
                # put the kth element into the hashset:
                hashset.add(nums[k])
    
    ans = [list(t) for t in st]
    return ans

    # optimal O(n^3) O(no. of quadruplets)
    ans = []
    
    # sort the given array:
    nums.sort()
    
    # calculating the quadruplets:
    for i in range(n):
        if i > 0 and nums[i] == nums[i - 1]:
            continue
        for j in range(i + 1, n):
            if j > i + 1 and nums[j] == nums[j - 1]:
                continue
            
            k, l = j + 1, n - 1
            while k < l:
                current_sum = nums[i] + nums[j] + nums[k] + nums[l]
                
                if current_sum < target:
                    k += 1
                elif current_sum > target:
                    l -= 1
                else:
                    temp = [nums[i], nums[j], nums[k], nums[l]]
                    ans.append(temp)
                    k += 1
                    l -= 1
                    while k < l and nums[k] == nums[k - 1]:
                        k += 1
                    while k < l and nums[l] == nums[l + 1]:
                        l -= 1
    return ans
```
    
### [Largest Subarray with 0 Sum](https://takeuforward.org/data-structure/length-of-the-longest-subarray-with-zero-sum/)
```cpp
int solve(vector<int>& a) {
	int maxLen = 0;
	unordered_map<int, int> mpp;
	int sum = 0;

	// optimal O(n) O(n)
	for(int i = 0;i<n;i++) {
		sum += A[i];
		if(sum == 0) {
			maxLen = i + 1;
		}
		else {
			if(mpp.find(sum) != mpp.end()) {
				maxLen = max(maxLen, i - mpp[sum]);
			}
			else {
				mpp[sum] = i;
			}
		}
	}

	return maxLen;
}

```

```python
def solve(a):
    n = len(a)
    maxLen = 0
    mpp = {}
    sum_val = 0

    # optimal O(n) O(n)
    for i in range(n):
        sum_val += a[i]
        if sum_val == 0:
            maxLen = i + 1
        else:
            if sum_val in mpp:
                maxLen = max(maxLen, i - mpp[sum_val])
            else:
                mpp[sum_val] = i

    return maxLen
```
    
### [Count number of subarrays with given xor K](https://takeuforward.org/data-structure/count-the-number-of-subarrays-with-given-xor-k/)
```cpp
int subarraysWithXorK(vector<int> a, int k) {
	int n = a.size(); //size of the given array.
	int cnt = 0;

	// brute force O(n^2) O(1)
	for (int i = 0; i < n; i++) {
		int xorr = 0;
		for (int j = i; j < n; j++) {
			xorr = xorr ^ a[j];
			if (xorr == k) cnt++;
		}
	}

	// optimal O(nlogn) O(n)
	int xr = 0;
	map<int, int> mpp;
	mpp[xr]++; //setting the value of 0.
	int cnt = 0;

	for (int i = 0; i < n; i++) {
		// prefix XOR till index i:
		xr = xr ^ a[i];

		//By formula: x = xr^k:
		int x = xr ^ k;
		cnt += mpp[x];

		// Insert the prefix xor till index i
		mpp[xr]++;
	}
	return cnt;
}

```

```python
def subarraysWithXorK(a, k):
    n = len(a)  # size of the given array.
    
    # brute force O(n^2) O(1)
    cnt = 0
    for i in range(n):
        xorr = 0
        for j in range(i, n):
            xorr = xorr ^ a[j]
            if xorr == k:
                cnt += 1
    return cnt

    # optimal O(nlogn) O(n)
    xr = 0
    mpp = {}
    mpp[xr] = 1  # setting the value of 0.
    cnt = 0

    for i in range(n):
        # prefix XOR till index i:
        xr = xr ^ a[i]

        # By formula: x = xr^k:
        x = xr ^ k
        cnt += mpp.get(x, 0)

        # Insert the prefix xor till index i
        mpp[xr] = mpp.get(xr, 0) + 1
    return cnt
```
    
### [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)
```cpp
vector<vector<int>> mergeOverlappingIntervals(vector<vector<int>> &arr) {
	int n = arr.size();
	sort(arr.begin(), arr.end());
	vector<vector<int>> ans;

	// brute force O(nlogn + 2*n) O(n)
	for (int i = 0; i < n; i++) { // select an interval:
		int start = arr[i][0];
		int end = arr[i][1];

		//Skip all the merged intervals:
		if (!ans.empty() && end <= ans.back()[1])
			continue;

		//check the rest of the intervals:
		for (int j = i + 1; j < n; j++) {
			if (arr[j][0] <= end)
				end = max(end, arr[j][1]);
			else
				break;
		}
		ans.push_back({start, end});
	}

	// optimal O(nlogn + n) O(n)
	for (int i = 0; i < n; i++) {
		if (ans.empty() || arr[i][0] > ans.back()[1]) {
			ans.push_back(arr[i]);
		} else {
			ans.back()[1] = max(ans.back()[1], arr[i][1]);
		}
	}
	return ans;
}

```

```python
def mergeOverlappingIntervals(arr):
    n = len(arr)
    arr.sort()
    ans = []

    # brute force O(nlogn + 2*n) O(n)
    for i in range(n):  # select an interval:
        start = arr[i][0]
        end = arr[i][1]
    
        # Skip all the merged intervals:
        if ans and end <= ans[-1][1]:
            continue
    
        # check the rest of the intervals:
        for j in range(i + 1, n):
            if arr[j][0] <= end:
                end = max(end, arr[j][1])
            else:
                break
        ans.append([start, end])
    return ans

    # optimal O(nlogn + n) O(n)
    for i in range(n):
        if not ans or arr[i][0] > ans[-1][1]:
            ans.append(arr[i])
        else:
            ans[-1][1] = max(ans[-1][1], arr[i][1])
    return ans
```
    
### [Merge two sorted arrays without extra space](https://takeuforward.org/data-structure/merge-two-sorted-arrays-without-extra-space/)
```cpp
void merge(long long arr1[], long long arr2[], int n, int m) {
	// brute force O(n+m) O(n+m)
	long long arr3[n + m];
	int left = 0;
	int right = 0;
	int index = 0;

	while (left < n && right < m) {
		if (arr1[left] <= arr2[right])
			arr3[index++] = arr1[left++];
		else
			arr3[index++] = arr2[right++];
	}

	while (left < n)
		arr3[index++] = arr1[left++];

	while (right < m)
		arr3[index++] = arr2[right++];

	for (int i = 0; i < n + m; i++) {
		if (i < n) arr1[i] = arr3[i];
		else arr2[i - n] = arr3[i];
	}

	// optimal O(min(n, m) + nlogn + mlogm) O(1)
	int left = n - 1;
	int right = 0;

	//Swap the elements until arr1[left] is
	// smaller than arr2[right]:
	while (left >= 0 && right < m) {
		if (arr1[left] > arr2[right]) {
			swap(arr1[left], arr2[right]);
			left--, right++;
		}
		else {
			break;
		}
	}

	sort(arr1, arr1 + n);
	sort(arr2, arr2 + m);

}

// optimal O(log(m+n) * (m+n)) O(1)
void swapIfGreater(long long arr1[], long long arr2[], int ind1, int ind2) {
	if (arr1[ind1] > arr2[ind2]) {
		swap(arr1[ind1], arr2[ind2]);
	}
}

void merge(long long arr1[], long long arr2[], int n, int m) {
	// len of the imaginary single array:
	int len = n + m;

	// Initial gap:
	int gap = (len / 2) + (len % 2);

	while (gap > 0) {
		// Place 2 pointers:
		int left = 0;
		int right = left + gap;
		while (right < len) {
			// case 1: left in arr1[]
			//and right in arr2[]:
			if (left < n && right >= n) {
				swapIfGreater(arr1, arr2, left, right - n);
			}
			// case 2: both pointers in arr2[]
			else if (left >= n) {
				swapIfGreater(arr2, arr2, left - n, right - n);
			// case 3: both pointers in arr1[]
			else
				swapIfGreater(arr1, arr1, left, right);
			left++, right++;
		}
		// break if iteration gap=1 is completed:
		if (gap == 1) break;

		// Otherwise, calculate new gap:
		gap = (gap / 2) + (gap % 2);
	}
}

```

```python
def merge_brute_force(arr1, arr2, n, m):
    # brute force O(n+m) O(n+m)
    arr3 = [0] * (n + m)
    left, right, index = 0, 0, 0

    while left < n and right < m:
        if arr1[left] <= arr2[right]:
            arr3[index] = arr1[left]
            left += 1
        else:
            arr3[index] = arr2[right]
            right += 1
        index += 1

    while left < n:
        arr3[index] = arr1[left]
        left += 1
        index += 1

    while right < m:
        arr3[index] = arr2[right]
        right += 1
        index += 1

    for i in range(n + m):
        if i < n:
            arr1[i] = arr3[i]
        else:
            arr2[i - n] = arr3[i]


def merge_optimal_sort(arr1, arr2, n, m):
    # optimal O(min(n, m) + nlogn + mlogm) O(1)
    left = n - 1
    right = 0

    # Swap the elements until arr1[left] is
    # smaller than arr2[right]:
    while left >= 0 and right < m:
        if arr1[left] > arr2[right]:
            arr1[left], arr2[right] = arr2[right], arr1[left]
            left -= 1
            right += 1
        else:
            break

    arr1.sort()
    arr2.sort()


def swapIfGreater(arr1, arr2, ind1, ind2):
    if arr1[ind1] > arr2[ind2]:
        arr1[ind1], arr2[ind2] = arr2[ind2], arr1[ind1]


def merge_optimal_gap(arr1, arr2, n, m):
    # optimal O(log(m+n) * (m+n)) O(1)
    # len of the imaginary single array:
    length = n + m

    # Initial gap:
    gap = (length // 2) + (length % 2)

    while gap > 0:
        # Place 2 pointers:
        left = 0
        right = left + gap
        while right < length:
            # case 1: left in arr1[] and right in arr2[]:
            if left < n and right >= n:
                swapIfGreater(arr1, arr2, left, right - n)
            # case 2: both pointers in arr2[]
            elif left >= n:
                swapIfGreater(arr2, arr2, left - n, right - n)
            # case 3: both pointers in arr1[]
            else:
                swapIfGreater(arr1, arr1, left, right)
            left += 1
            right += 1

        # break if iteration gap=1 is completed:
        if gap == 1:
            break

        # Otherwise, calculate new gap:
        gap = (gap // 2) + (gap % 2)
```
    
### [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)
```cpp
void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
	// brute force O((m+n)log(m+n)) O(1)
	for (int j = 0, i = m; j<n; i++, j++)
		nums1[i] = nums2[j];
	sort(nums1.begin(),nums1.end());

	// two pointer O(m+n) O(1)
	int i = m - 1;
	int j = n - 1;
	int k = m + n - 1;

	while (j >= 0) {
		if (i >= 0 && nums1[i] > nums2[j])
			nums1[k--] = nums1[i--];
		else
			nums1[k--] = nums2[j--];
	}
}

```

```python
def merge(nums1, m, nums2, n):
    # brute force O((m+n)log(m+n)) O(1)
    for j in range(n):
        nums1[m + j] = nums2[j]
    nums1.sort()

    # two pointer O(m+n) O(1)
    i = m - 1
    j = n - 1
    k = m + n - 1

    while j >= 0:
        if i >= 0 and nums1[i] > nums2[j]:
            nums1[k] = nums1[i]
            k -= 1
            i -= 1
        else:
            nums1[k] = nums2[j]
            k -= 1
            j -= 1
```
    
### [Find the repeating and missing number](https://takeuforward.org/data-structure/find-the-repeating-and-missing-numbers/)
```cpp
vector<int> findMissingRepeatingNumbers(vector<int> a) {
	int n = a.size(); // size of the array
	int repeating = -1, missing = -1;

	// brute force O(n^2) O(1)
	for (int i = 1; i <= n; i++) {
		int cnt = 0;
		for (int j = 0; j < n; j++)
			if (a[j] == i) cnt++;

		if (cnt == 2) repeating = i;
		else if (cnt == 0) missing = i;

		if (repeating != -1 && missing != -1)
			break;
	}

	// better O(n) O(n)
	int hash[n + 1] = {0}; // hash array

	for (int i = 0; i < n; i++)
		hash[a[i]]++;

	int repeating = -1, missing = -1;
	for (int i = 1; i <= n; i++) {
		if (hash[i] == 2) repeating = i;
		else if (hash[i] == 0) missing = i;

		if (repeating != -1 && missing != -1)
			break;
	}

	// optimal (math) O(n) O(1)
	long long SN = (n * (n + 1)) / 2;
	long long S2N = (n * (n + 1) * (2 * n + 1)) / 6;

	// Calculate S and S2:
	long long S = 0, S2 = 0;
	for (int i = 0; i < n; i++) {
		S += a[i];
		S2 += (long long)a[i] * (long long)a[i];
	}

	//S-Sn = X-Y:
	long long val1 = S - SN;

	// S2-S2n = X^2-Y^2:
	long long val2 = S2 - S2N;

	//Find X+Y = (X^2-Y^2)/(X-Y):
	val2 = val2 / val1;

	//Find X and Y: X = ((X+Y)+(X-Y))/2 and Y = X-(X-Y),
	// Here, X-Y = val1 and X+Y = val2:
	long long x = (val1 + val2) / 2;
	long long y = x - val1;
	repeating = x, missing = y;

	return {repeating, missing};

	// optimal (xor)
	int xr = 0;

	//Step 1: Find XOR of all elements:
	for (int i = 0; i < n; i++) {
		xr = xr ^ a[i];
		xr = xr ^ (i + 1);
	}

	//Step 2: Find the differentiating bit number:
	int number = (xr & ~(xr - 1));

	//Step 3: Group the numbers:
	int zero = 0;
	int one = 0;
	for (int i = 0; i < n; i++) {
		//part of 1 group:
		if ((a[i] & number) != 0) {
			one = one ^ a[i];
		}
		//part of 0 group:
		else {
			zero = zero ^ a[i];
		}
	}

	for (int i = 1; i <= n; i++) {
		//part of 1 group:
		if ((i & number) != 0) {
			one = one ^ i;
		}
		//part of 0 group:
		else {
			zero = zero ^ i;
		}
	}

	// Last step: Identify the numbers:
	int cnt = 0;
	for (int i = 0; i < n; i++) {
		if (a[i] == zero) cnt++;
	}

	if (cnt == 2) return {zero, one};
	return {one, zero};
}

```

```python
def findMissingRepeatingNumbers(a):
    n = len(a)  # size of the array

    # brute force O(n^2) O(1)
    repeating = -1
    missing = -1
    for i in range(1, n + 1):
        cnt = 0
        for j in range(n):
            if a[j] == i:
                cnt += 1
    
        if cnt == 2:
            repeating = i
        elif cnt == 0:
            missing = i
    
        if repeating != -1 and missing != -1:
            break
    
    return [repeating, missing]

    # better O(n) O(n)
    hash_array = [0] * (n + 1)  # hash array
    
    for i in range(n):
        hash_array[a[i]] += 1
    
    repeating = -1
    missing = -1
    for i in range(1, n + 1):
        if hash_array[i] == 2:
            repeating = i
        elif hash_array[i] == 0:
            missing = i
    
        if repeating != -1 and missing != -1:
            break
    
    return [repeating, missing]

    # optimal (math) O(n) O(1)
    # long long is not necessary in Python as integers have arbitrary precision
    SN = (n * (n + 1)) // 2
    S2N = (n * (n + 1) * (2 * n + 1)) // 6
    
    # Calculate S and S2:
    S = sum(a)
    S2 = sum(x * x for x in a)
    
    # S-Sn = X-Y:
    val1 = S - SN
    
    # S2-S2n = X^2-Y^2:
    val2 = S2 - S2N
    
    # Find X+Y = (X^2-Y^2)/(X-Y):
    val2 = val2 // val1
    
    # Find X and Y: X = ((X+Y)+(X-Y))/2 and Y = X-(X-Y),
    # Here, X-Y = val1 and X+Y = val2:
    x = (val1 + val2) // 2
    y = x - val1
    repeating = x
    missing = y
    
    return [int(repeating), int(missing)]
    
    # optimal (xor) O(n) O(1)
    xr = 0

    # Step 1: Find XOR of all elements:
    for i in range(n):
        xr = xr ^ a[i]
        xr = xr ^ (i + 1)

    # Step 2: Find the differentiating bit number:
    number = xr & -xr

    # Step 3: Group the numbers:
    zero = 0
    one = 0
    for i in range(n):
        # part of 1 group:
        if (a[i] & number) != 0:
            one = one ^ a[i]
        # part of 0 group:
        else:
            zero = zero ^ a[i]

    for i in range(1, n + 1):
        # part of 1 group:
        if (i & number) != 0:
            one = one ^ i
        # part of 0 group:
        else:
            zero = zero ^ i

    # Last step: Identify the numbers:
    cnt = 0
    for i in range(n):
        if a[i] == zero:
            cnt += 1

    if cnt == 2:
        return [zero, one]
    return [one, zero]
```
### [Count Inversions](https://takeuforward.org/data-structure/count-inversions-in-an-array/)
```cpp
// brute force O(n^2) O(1)
int numberOfInversions(vector<int>&a, int n) {
	int cnt = 0;
	for (int i = 0; i < n; i++) {
		for (int j = i + 1; j < n; j++) {
			if (a[i] > a[j]) cnt++;
		}
	}
	return cnt;
}

// optimal O(nlogn) O(n)
int merge(vector<int> &arr, int low, int mid, int high) {
	vector<int> temp; // temporary array
	int left = low;      // starting index of left half of arr
	int right = mid + 1;   // starting index of right half of arr

	//Modification 1: cnt variable to count the pairs:
	int cnt = 0;

	//storing elements in the temporary array in a sorted manner//
	while (left <= mid && right <= high) {
		if (arr[left] <= arr[right]) {
			temp.push_back(arr[left]);
			left++;
		}
		else {
			temp.push_back(arr[right]);
			cnt += (mid - left + 1); //Modification 2
			right++;
		}
	}

	// if elements on the left half are still left //

	while (left <= mid) {
		temp.push_back(arr[left]);
		left++;
	}

	//  if elements on the right half are still left //
	while (right <= high) {
		temp.push_back(arr[right]);
		right++;
	}

	// transfering all elements from temporary to arr //
	for (int i = low; i <= high; i++) {
		arr[i] = temp[i - low];
	}

	return cnt; // Modification 3
}

int mergeSort(vector<int> &arr, int low, int high) {
	int cnt = 0;
	if (low >= high) return cnt;
	int mid = (low + high) / 2 ;
	cnt += mergeSort(arr, low, mid);  // left half
	cnt += mergeSort(arr, mid + 1, high); // right half
	cnt += merge(arr, low, mid, high);  // merging sorted halves
	return cnt;
}

int numberOfInversions(vector<int>&a, int n) {
	return mergeSort(a, 0, n - 1);
}

```

```python
# brute force O(n^2) O(1)
def numberOfInversions_brute(a, n):
    cnt = 0
    for i in range(n):
        for j in range(i + 1, n):
            if a[i] > a[j]:
                cnt += 1
    return cnt

# optimal O(nlogn) O(n)
def merge(arr, low, mid, high):
    temp = []  # temporary array
    left = low  # starting index of left half of arr
    right = mid + 1  # starting index of right half of arr

    # Modification 1: cnt variable to count the pairs:
    cnt = 0

    # storing elements in the temporary array in a sorted manner
    while left <= mid and right <= high:
        if arr[left] <= arr[right]:
            temp.append(arr[left])
            left += 1
        else:
            temp.append(arr[right])
            cnt += (mid - left + 1)  # Modification 2
            right += 1

    # if elements on the left half are still left
    while left <= mid:
        temp.append(arr[left])
        left += 1

    # if elements on the right half are still left
    while right <= high:
        temp.append(arr[right])
        right += 1

    # transferring all elements from temporary to arr
    for i in range(low, high + 1):
        arr[i] = temp[i - low]

    return cnt  # Modification 3

def mergeSort(arr, low, high):
    cnt = 0
    if low >= high:
        return cnt
    mid = (low + high) // 2
    cnt += mergeSort(arr, low, mid)  # left half
    cnt += mergeSort(arr, mid + 1, high)  # right half
    cnt += merge(arr, low, mid, high)  # merging sorted halves
    return cnt

def numberOfInversions_optimal(a, n):
    return mergeSort(a, 0, n - 1)
```
    
### [493. Reverse Pairs](https://leetcode.com/problems/reverse-pairs/)
```cpp
// brute force O(n^2) O(1)
int countPairs(vector<int>&a, int n) {
	int cnt = 0;
	for (int i = 0; i < n; i++) {
		for (int j = i + 1; j < n; j++) {
			if (a[i] > 2 * a[j]) cnt++;
		}
	}
	return cnt;
}

// optimal O(nlogn) O(n)
void merge(vector<int> &arr, int low, int mid, int high) {
	vector<int> temp; // temporary array
	int left = low;      // starting index of left half of arr
	int right = mid + 1;   // starting index of right half of arr

	//storing elements in the temporary array in a sorted manner//

	while (left <= mid && right <= high) {
		if (arr[left] <= arr[right]) {
			temp.push_back(arr[left]);
			left++;
		}
		else {
			temp.push_back(arr[right]);
			right++;
		}
	}

	// if elements on the left half are still left //

	while (left <= mid) {
		temp.push_back(arr[left]);
		left++;
	}

	//  if elements on the right half are still left //
	while (right <= high) {
		temp.push_back(arr[right]);
		right++;
	}

	// transfering all elements from temporary to arr //
	for (int i = low; i <= high; i++) {
		arr[i] = temp[i - low];
	}
}

int countPairs(vector<int> &arr, int low, int mid, int high) {
	int right = mid + 1;
	int cnt = 0;
	for (int i = low; i <= mid; i++) {
		while (right <= high && (long long)arr[i] > (long long)2 * arr[right]) right++;
		cnt += (right - (mid + 1));
	}
	return cnt;
}

int mergeSort(vector<int> &arr, int low, int high) {
	int cnt = 0;
	if (low >= high) return cnt;
	int mid = (low + high) / 2 ;
	cnt += mergeSort(arr, low, mid);  // left half
	cnt += mergeSort(arr, mid + 1, high); // right half
	cnt += countPairs(arr, low, mid, high); //Modification
	merge(arr, low, mid, high);  // merging sorted halves
	return cnt;
}

int team(vector <int> & skill, int n) {
	return mergeSort(skill, 0, n - 1);
}

```

```python
# brute force O(n^2) O(1)
def countPairs_brute(a, n):
    cnt = 0
    for i in range(n):
        for j in range(i + 1, n):
            if a[i] > 2 * a[j]:
                cnt += 1
    return cnt

# optimal O(nlogn) O(n)
def merge(arr, low, mid, high):
    temp = []  # temporary array
    left = low  # starting index of left half of arr
    right = mid + 1  # starting index of right half of arr

    # storing elements in the temporary array in a sorted manner
    while left <= mid and right <= high:
        if arr[left] <= arr[right]:
            temp.append(arr[left])
            left += 1
        else:
            temp.append(arr[right])
            right += 1

    # if elements on the left half are still left
    while left <= mid:
        temp.append(arr[left])
        left += 1

    # if elements on the right half are still left
    while right <= high:
        temp.append(arr[right])
        right += 1

    # transferring all elements from temporary to arr
    for i in range(low, high + 1):
        arr[i] = temp[i - low]

def countPairs_merge(arr, low, mid, high):
    right = mid + 1
    cnt = 0
    for i in range(low, mid + 1):
        while right <= high and arr[i] > 2 * arr[right]:
            right += 1
        cnt += (right - (mid + 1))
    return cnt

def mergeSort(arr, low, high):
    cnt = 0
    if low >= high:
        return cnt
    mid = (low + high) // 2
    cnt += mergeSort(arr, low, mid)  # left half
    cnt += mergeSort(arr, mid + 1, high)  # right half
    cnt += countPairs_merge(arr, low, mid, high)  # Modification
    merge(arr, low, mid, high)  # merging sorted halves
    return cnt

def team(skill, n):
    return mergeSort(skill, 0, n - 1)
```

# Moore’s Voting Algorithm
### [169. Majority Element](https://leetcode.com/problems/majority-element/)
   ![image.png](image%202.png)
  
![image.png](image%203.png)
    
![image.png](image%204.png)

![image.png](image%205.png)
    
```cpp
int majorityElement(vector<int> v) {
	int n = v.size();

	// brute force O(n^2) O(1)
	for (int i = 0; i < n; i++) {
		int cnt = 0;
		for (int j = 0; j < n; j++) {
			if (v[j] == v[i]) {
				cnt++;
			}
		}

		if (cnt > (n / 2))
			return v[i];
	}
	return -1;

	// better O(nlogn) O(n)
	map<int, int> mpp;

	for (int i = 0; i < n; i++)
		mpp[v[i]]++;

	for (auto it : mpp) {
		if (it.second > (n / 2))
			return it.first;
	}

	return -1;

	// optimal (Moore’s Voting Algorithm) O(n) O(1)
	int cnt = 0; // count
	int el; // Element

	//applying the algorithm:
	for (int i = 0; i < n; i++) {
		if (cnt == 0) {
			cnt = 1;
			el = v[i];
		}
		else if (el == v[i]) cnt++;
		else cnt--;
	}

	//checking if the stored element is the majority element:
	for (int i=0; i<n; i++) {
		if (el == v[i])
			return v[i];
	}
	return -1;
}

```

```python
def majorityElement(v):
    n = len(v)

    # brute force O(n^2) O(1)
    for i in range(n):
        cnt = 0
        for j in range(n):
            if v[j] == v[i]:
                cnt += 1
        if cnt > (n / 2):
            return v[i]
    return -1

    # better O(nlogn) O(n)
    mpp = {}
    for i in range(n):
        mpp[v[i]] = mpp.get(v[i], 0) + 1
    
	for key, value in mpp.items():
        if value > (n / 2):
            return key
    return -1

    # optimal (Moore’s Voting Algorithm) O(n) O(1)
    cnt = 0  # count
    el = None  # Element

    # applying the algorithm:
    for i in range(n):
        if cnt == 0:
            cnt = 1
            el = v[i]
        elif el == v[i]:
            cnt += 1
        else:
            cnt -= 1

    # checking if the stored element is the majority element:
    # A second pass is not strictly needed for this problem as a majority element is guaranteed to exist.
    # However, if there might not be a majority element, this check is necessary.
    cnt = 0
    for i in range(n):
        if el == v[i]:
            cnt += 1
    if cnt > (n // 2):
        return el
    return -1
```
    
### [229. Majority Element II](https://leetcode.com/problems/majority-element-ii/)    
![image.png](image%206.png)
    
![image.png](image%207.png)
    
```cpp
vector<int> majorityElement(vector<int> v) {
	int n = v.size(); //size of the array
	vector<int> ls; // list of answers

	// brute force O(n^2) O(1)
	for (int i = 0; i < n; i++) {
		if (ls.size() == 0 || ls[0] != v[i]) {
			int cnt = 0;
			for (int j = 0; j < n; j++) {
				if (v[j] == v[i]) {
					cnt++;
				}
			}
			if (cnt > (n / 3))
				ls.push_back(v[i]);
		}
		if (ls.size() == 2) break;
	}

	// better O(nlogn) O(n)
	map<int, int> mpp;

	int mini = int(n / 3) + 1;

	for (int i = 0; i < n; i++) {
		mpp[v[i]]++;

		if (mpp[v[i]] == mini) {
			ls.push_back(v[i]);
		}
		if (ls.size() == 2) break;
	}

	// optimal (moor's voting algo) O(n) O(1)
	int cnt1 = 0, cnt2 = 0; // counts
	int el1 = INT_MIN; // element 1
	int el2 = INT_MIN; // element 2

	// applying the Extended Boyer Moore's Voting Algorithm:
	for (int i = 0; i < n; i++) {
		if (cnt1 == 0 && el2 != v[i]) {
			cnt1 = 1;
			el1 = v[i];
		}
		else if (cnt2 == 0 && el1 != v[i]) {
			cnt2 = 1;
			el2 = v[i];
		}
		else if (v[i] == el1) cnt1++;
		else if (v[i] == el2) cnt2++;
		else {
			cnt1--, cnt2--;
		}
	}

	// Manually check if the stored elements in
	// el1 and el2 are the majority elements:
	cnt1 = 0, cnt2 = 0;
	for (int i = 0; i < n; i++) {
		if (v[i] == el1) cnt1++;
		if (v[i] == el2) cnt2++;
	}

	int mini = int(n / 3) + 1;
	if (cnt1 >= mini) ls.push_back(el1);
	if (cnt2 >= mini) ls.push_back(el2);

	// Uncomment the following line
	// if it is told to sort the answer array:
	// sort(ls.begin(), ls.end()); //TC --> O(2*log2) ~ O(1);

	return ls;
}

```

```python
import math

def majorityElement(v):
    n = len(v)  # size of the array
    ls = []  # list of answers

    # brute force O(n^2) O(1)
    for i in range(n):
        if len(ls) == 0 or ls[0] != v[i]:
            cnt = 0
            for j in range(n):
                if v[j] == v[i]:
                    cnt += 1
            if cnt > (n / 3):
                ls.append(v[i])
        if len(ls) == 2:
            break
    
    return ls

    # better O(nlogn) O(n)
    mpp = {}
    mini = math.floor(n / 3) + 1
    
    for i in range(n):
        mpp[v[i]] = mpp.get(v[i], 0) + 1
    
        if mpp[v[i]] == mini:
            ls.append(v[i])
    
        if len(ls) == 2:
            break
    
    return ls

    # optimal (moor's voting algo) O(n) O(1)
    cnt1, cnt2 = 0, 0  # counts
    el1, el2 = float('-inf'), float('-inf')  # element 1, element 2

    # applying the Extended Boyer Moore's Voting Algorithm:
    for i in range(n):
        if cnt1 == 0 and el2 != v[i]:
            cnt1 = 1
            el1 = v[i]
        elif cnt2 == 0 and el1 != v[i]:
            cnt2 = 1
            el2 = v[i]
        elif v[i] == el1:
            cnt1 += 1
        elif v[i] == el2:
            cnt2 += 1
        else:
            cnt1 -= 1
            cnt2 -= 1

    # Manually check if the stored elements in
    # el1 and el2 are the majority elements:
    cnt1, cnt2 = 0, 0
    for i in range(n):
        if v[i] == el1:
            cnt1 += 1
        if v[i] == el2:
            cnt2 += 1

    mini = math.floor(n / 3) + 1
    if cnt1 >= mini:
        ls.append(el1)
    if cnt2 >= mini:
        ls.append(el2)

    # Uncomment the following line
    # if it is told to sort the answer array:
    # ls.sort()

    return ls
```
    
# Kadane's Algorithm
### Find a non-empty sub-array with largest sum or return indices of max sum window
```python
# Brute Force: O(n^2)
def bruteForce(nums):
    maxSum = nums[0]

    for i in range(len(nums)):
        curSum = 0
        for j in range(i, len(nums)):
            curSum += nums[j]
            maxSum = max(maxSum, curSum)
    return maxSum

# Kadane's Algorithm: O(n)
def kadanes(nums):
    maxSum = nums[0]
    curSum = 0

    for n in nums:
        curSum += max(curSum, 0) + n
        maxSum = max(maxSum, curSum)
    return maxSum

# Return the left and right index of the max subarray sum,
# assuming there's exactly one result (no ties).
# Sliding window variation of Kadane's: O(n)
def slidingWindow(nums):
    maxSum = nums[0]
    curSum = 0
    maxL, maxR = 0, 0
    L = 0

    for R in range(len(nums)):
        if curSum < 0:
            curSum = 0
            L = R

        curSum += nums[R]
        if curSum > maxSum:
            maxSum = curSum
            maxL, maxR = L, R 

    return [maxL, maxR]
```
### [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
```cpp
long long maxSubarraySum(int arr[], int n) {
	long long maxi = INT_MIN;

	// brute force O(n^2) O(1)
	for (int i = 0; i < n; i++) {
		int sum = 0;
		for (int j = i; j < n; j++) {
			sum += arr[j];
			maxi = max(maxi, sum);
		}
	}
	return maxi;

	// optimal O(n) O(1)
	long long sum = 0;

	for (int i = 0; i < n; i++) {
		sum += arr[i];
		maxi = max(maxi, sum);

		if (sum < 0) sum = 0;
	}
	return maxi;

	// return start and end index
	int start = 0;
	int ansStart = -1, ansEnd = -1;
	for (int i = 0; i < n; i++) {
		if (sum == 0) start = i;
		sum += arr[i];

		if (sum > maxi) {
			maxi = sum;
			ansStart = start;
			ansEnd = i;
		}

		if (sum < 0) sum = 0;
	}
	return {ansStart, ansEnd};
}

```

```python
import sys

def maxSubarraySum(arr, n):
    maxi = -sys.maxsize - 1

    # brute force O(n^2) O(1)
    for i in range(n):
        sum_val = 0
        for j in range(i, n):
            sum_val += arr[j]
            maxi = max(maxi, sum_val)
    return maxi

    # optimal O(n) O(1)
    sum_val = 0
    maxi = -sys.maxsize - 1

    for i in range(n):
        sum_val += arr[i]
        maxi = max(maxi, sum_val)

        if sum_val < 0:
            sum_val = 0
    return maxi

    # return start and end index
    start = 0
    ansStart, ansEnd = -1, -1
    sum_val = 0
    maxi = -sys.maxsize - 1
    
    for i in range(n):
        if sum_val == 0:
            start = i
        sum_val += arr[i]
    
        if sum_val > maxi:
            maxi = sum_val
            ansStart = start
            ansEnd = i
    
        if sum_val < 0:
            sum_val = 0
    
    return [ansStart, ansEnd]
```
    
### [152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)
```cpp
int maxProductSubArray(vector<int>& nums) {
	// brute force O(n^2) O(1)
	int result = nums[0];
	for(int i=0;i<nums.size()-1;i++) {
		int p = nums[i];
		for(int j=i+1;j<nums.size();j++) {
		   result = max(result,p);
		   p *= nums[j];
		}
		result = max(result,p);//manages (n-1)th term
	}
	return result;

	// optimal O(n) O(1)
	int pre = 1, suff = 1;
	int ans = INT_MIN;
	for (int i = 0; i < n; i++) {
		if (pre == 0) pre = 1;
		if (suff == 0) suff = 1;
		pre *= arr[i];
		suff *= arr[n - i - 1];
		ans = max(ans, max(pre, suff));
	}
	return ans;

	// optimal (kadane's algo) O(n) O(1)
	int prod1 = nums[0], prod2 = nums[0], result = nums[0];

	for(int i=1;i<nums.size();i++) {
		int temp = max({nums[i],prod1*nums[i],prod2*nums[i]});
		prod2 = min({nums[i],prod1*nums[i],prod2*nums[i]});
		prod1 = temp;

		result = max(result,prod1);
	}

	return result;
}

```

```python
import math

def maxProductSubArray(nums):
    n = len(nums)

    # brute force O(n^2) O(1)
    result = nums[0]
    for i in range(n):
        p = 1
        for j in range(i, n):
            p *= nums[j]
            result = max(result, p)
    return result

    # optimal O(n) O(1)
    pre = 1
    suff = 1
    ans = float('-inf')
    for i in range(n):
        if pre == 0:
            pre = 1
        if suff == 0:
            suff = 1
        pre *= nums[i]
        suff *= nums[n - i - 1]
        ans = max(ans, max(pre, suff))
    return ans

    # optimal (kadane's algo) O(n) O(1)
    prod1 = nums[0]
    prod2 = nums[0]
    result = nums[0]
    
    for i in range(1, n):
        temp = max(nums[i], prod1 * nums[i], prod2 * nums[i])
        prod2 = min(nums[i], prod1 * nums[i], prod2 * nums[i])
        prod1 = temp
    
        result = max(result, prod1)
    
    return result
```
    
# Sliding Window Fixed
### Given an array return true if there are two elements within a window of size k that are equal 
```python
# Check if array contains a pair of duplicate values,
# where the two duplicates are no farther than k positions from 
# eachother (i.e. arr[i] == arr[j] and abs(i - j) + 1 <= k).
# Brute force O(n * k)
def closeDuplicatesBruteForce(nums, k):
    for L in range(len(nums)):
        for R in range(L + 1, min(len(nums), L + k)):
            if nums[L] == nums[R]:
                return True
    return False

# Same problem using sliding window.
# O(n)
def closeDuplicates(nums, k):
    window = set() # Cur window of size <= k
    L = 0

    for R in range(len(nums)):
        if R - L + 1 > k:
            window.remove(nums[L])
            L += 1
        if nums[R] in window:
            return True
        window.add(nums[R])

    return False
```
# Sliding Window Variable  
#### Find the length of longest subarray with the same value in each position
```python
#  O(n)
def longestSubarray(nums):
    length = 0
    L = 0
    
    for R in range(len(nums)):
        if nums[L] != nums[R]:
            L = R 
        length = max(length, R - L + 1)
    return length
```
#### Find length of the minimum size subarray where the sum is greater than or equal to the target. Assume all values in the input are positive. 
```python
# O(n)
def shortestSubarray(nums, target):
    L, total = 0, 0
    length = float("inf")
    
    for R in range(len(nums)):
        total += nums[R]
        while total >= target:
            length = min(R - L + 1, length)
            total -= nums[L]
            L += 1
    return 0 if length == float("inf") else length
```
#### [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        maxP = 0

		# brute force O(n^2) O(1)
        for i in range(len(prices)):
            buy = prices[i]
            for j in range(i + 1, len(prices)):
                sell  = prices[j]
                maxP = max(maxP, sell - buy)
        return maxP

		# two pointers O(n) O(1)
		l, r = 0, 1
		
		while r < len(prices):
            if prices[l] < prices[r]:
                profit = prices[r] - prices[l]
                maxP = max(maxP, profit)
            else:
                l = r
            r += 1
        return maxP


		# Dynamic Programming O(n) O(1)
		minBuy = prices[0]

        for sell in prices:
            maxP = max(maxP, sell - minBuy)
            minBuy = min(minBuy, sell)
        return maxP
```
#### [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        res = 0

		# brute force O(n∗m) O(m)
		# Where n is the length of the string and m is the total number of unique characters in the string.
        for i in range(len(s)):
            charSet = set()
            for j in range(i, len(s)):
                if s[j] in charSet:
                    break
                charSet.add(s[j])
            res = max(res, len(charSet))
        return res

		# Sliding Window O(n) O(m)
		charSet = set()
        l = 0
	
		for r in range(len(s)):
            while s[r] in charSet:
                charSet.remove(s[l])
                l += 1
            charSet.add(s[r])
            res = max(res, r - l + 1)
        return res

		# Sliding Window (Optimal) O(n) O(m) ignored
		mp = {}
        l = 0
	
		for r in range(len(s)):
            if s[r] in mp:
                l = max(mp[s[r]] + 1, l)
            mp[s[r]] = r
            res = max(res, r - l + 1)
        return res
```
#### [424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)  
```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        res = 0

		# brute force O(n^2) O(m)
		# Where n is the length of the string and m is the total number of unique characters in the string.
		for i in range(len(s)):
            count, maxf = {}, 0
            for j in range(i, len(s)):
                count[s[j]] = 1 + count.get(s[j], 0)
                maxf = max(maxf, count[s[j]])
                if (j - i + 1) - maxf <= k:
                    res = max(res, j - i + 1)
        return res

		# Sliding Window O(m∗n) O(m)
		charSet = set(s)

        for c in charSet:
            count = l = 0
            for r in range(len(s)):
                if s[r] == c:
                    count += 1

                while (r - l + 1) - count > k:
                    if s[l] == c:
                        count -= 1
                    l += 1
                    
                res = max(res, r - l + 1)
        return res		

		# Sliding Window (Optimal) O(n) O(m)
		count = {}
        
        l = 0
        maxf = 0
        for r in range(len(s)):
            count[s[r]] = 1 + count.get(s[r], 0)
            maxf = max(maxf, count[s[r]])

            while (r - l + 1) - maxf > k:
                count[s[l]] -= 1
                l += 1
            res = max(res, r - l + 1)

        return res
```
#### [567. Permutation in String](https://leetcode.com/problems/permutation-in-string/)
```python
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
		if len(s1) > len(s2):
            return False

		# brute force O(n^3logn) O(n)
		s1 = sorted(s1)
        for i in range(len(s2)):
            for j in range(i, len(s2)):
                subStr = s2[i : j + 1]
                subStr = sorted(subStr)
                if subStr == s1:
                    return True
        return False

		# Hash Table O(n∗m) O(1) since we have at most 26 different characters.
		count1 = {}
        for c in s1:
            count1[c] = 1 + count1.get(c, 0)
        
        need = len(count1)
        for i in range(len(s2)):
            count2, cur = {}, 0
            for j in range(i, len(s2)):
                count2[s2[j]] = 1 + count2.get(s2[j], 0)
                if count1.get(s2[j], 0) < count2[s2[j]]:
                    break
                if count1.get(s2[j], 0) == count2[s2[j]]:
                    cur += 1
                if cur == need:
                    return True
        return False
	
		# Sliding Window O(n) O(1)
        s1Count, s2Count = [0] * 26, [0] * 26
        for i in range(len(s1)):
            s1Count[ord(s1[i]) - ord('a')] += 1
            s2Count[ord(s2[i]) - ord('a')] += 1
        
        matches = 0
        for i in range(26):
            matches += (1 if s1Count[i] == s2Count[i] else 0)
        
        l = 0
        for r in range(len(s1), len(s2)):
            if matches == 26:
                return True
            
            index = ord(s2[r]) - ord('a')
            s2Count[index] += 1
            if s1Count[index] == s2Count[index]:
                matches += 1
            elif s1Count[index] + 1 == s2Count[index]:
                matches -= 1

            index = ord(s2[l]) - ord('a')
            s2Count[index] -= 1
            if s1Count[index] == s2Count[index]:
                matches += 1
            elif s1Count[index] - 1 == s2Count[index]:
                matches -= 1
            l += 1
        return matches == 26
```
#### [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        if t == "":
            return ""

		# brute force O(n^2) O(m)
        countT = {}
        for c in t:
            countT[c] = 1 + countT.get(c, 0)

        res, resLen = [-1, -1], float("infinity")
        for i in range(len(s)):
            countS = {}
            for j in range(i, len(s)):
                countS[s[j]] = 1 + countS.get(s[j], 0)

                flag = True
                for c in countT:
                    if countT[c] > countS.get(c, 0):
                        flag = False
                        break
                
                if flag and (j - i + 1) < resLen:
                    resLen = j - i + 1
                    res = [i, j]

        l, r = res
        return s[l : r + 1] if resLen != float("infinity") else ""

		# sliding window O(n) O(m)
		countT, window = {}, {}
        for c in t:
            countT[c] = 1 + countT.get(c, 0)

        have, need = 0, len(countT)
        res, resLen = [-1, -1], float("infinity")
        l = 0
        for r in range(len(s)):
            c = s[r]
            window[c] = 1 + window.get(c, 0)

            if c in countT and window[c] == countT[c]:
                have += 1

            while have == need:
                if (r - l + 1) < resLen:
                    res = [l, r]
                    resLen = r - l + 1
                    
                window[s[l]] -= 1
                if s[l] in countT and window[s[l]] < countT[s[l]]:
                    have -= 1
                l += 1
        l, r = res
        return s[l : r + 1] if resLen != float("infinity") else ""
```
# Two pointer
#### Given a string of characters, return true if it's a palindrome return false otherwise 
```python
# O(n)
def isPalindrome(word):
    L, R = 0, len(word) - 1
    while L < R:
        if word[L] != word[R]:
            return False
        L += 1
        R -= 1
    return True
```
#### Given a sorted array of integers, return the indices of two elements (in different positions) that sum up to the target value. Assume there is exactly one solution
```python
def targetSum(nums, target):
    L, R = 0, len(nums) - 1
    while L < R:
        if nums[L] + nums[R] > target:
            R -= 1
        elif nums[L] + nums[R] < target:
            L += 1
        else:
            return [L, R]
```
#### [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
#### [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
```python
class Solution:
    def alphaNum(self, c):
        return (ord('A') <= ord(c) <= ord('Z') or 
                ord('a') <= ord(c) <= ord('z') or 
                ord('0') <= ord(c) <= ord('9')) 
                
    def isPalindrome(self, s: str) -> bool:
	# Reverse String [T-O(n), S-(n)]
        newStr = ''
        for c in s:
            if c.isalnum():
                newStr += c.lower()
        return newStr == newStr[::-1]

	# Two Pointers [T-O(n), S-(1)]
	l, r = 0, len(s) - 1

        while l < r:
            while l < r and not self.alphaNum(s[l]):
                l += 1
            while r > l and not self.alphaNum(s[r]):
                r -= 1
            if s[l].lower() != s[r].lower():
                return False
            l, r = l + 1, r - 1
        return True 
```
#### [167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
	# Brute Force [T-O(n^2), S-(1)]
        for i in range(len(numbers)):
            for j in range(i + 1, len(numbers)):
                if numbers[i] + numbers[j] == target:
                    return [i + 1, j + 1]
        return []

	# Binary Search [T-O(nlogn), S-(1)]
	for i in range(len(numbers)):
            l, r = i + 1, len(numbers) - 1
            tmp = target - numbers[i]
            while l <= r:
                mid = l + (r - l)//2
                if numbers[mid] == tmp:
                    return [i + 1, mid + 1]
                elif numbers[mid] < tmp:
                    l = mid + 1
                else:
                    r = mid - 1
        return []

	# Hash Map [T-O(n), S-(n)]
	mp = defaultdict(int)
        for i in range(len(numbers)):
            tmp = target - numbers[i]
            if mp[tmp]:
                return [mp[tmp], i + 1]
            mp[numbers[i]] = i + 1
        return []

	# Two Pointers [T-O(n), S-(1)]
	l, r = 0, len(numbers) - 1

        while l < r:
            curSum = numbers[l] + numbers[r]

            if curSum > target:
                r -= 1
            elif curSum < target:
                l += 1
            else:
                return [l + 1, r + 1]
        return [] 
```
#### [15. 3Sum](https://leetcode.com/problems/3sum/)
```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
	res = set()
        nums.sort()

        # Brute Force [T-O(n^3), S-O(m)]
	# Where mm is the number of triplets and nn is the length of the given array.
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                for k in range(j + 1, len(nums)):
                    if nums[i] + nums[j] + nums[k] == 0:
                        tmp = [nums[i], nums[j], nums[k]]
                        res.add(tuple(tmp))
        return [list(i) for i in res]

	# Hash Map [T-O(n^2), S-O(n)]
	count = defaultdict(int)
        for num in nums:
            count[num] += 1

		for i in range(len(nums)):
            count[nums[i]] -= 1
            if i and nums[i] == nums[i - 1]:
                continue

            for j in range(i + 1, len(nums)):
                count[nums[j]] -= 1
                if j - 1 > i and nums[j] == nums[j - 1]:
                    continue
                target = -(nums[i] + nums[j])
                if count[target] > 0:
                    res.append([nums[i], nums[j], target])

            for j in range(i + 1, len(nums)):
                count[nums[j]] += 1
        return res

	# Two Pointers [T-O(n), S-O(m)]
	for i, a in enumerate(nums):
            if a > 0:
                break

            if i > 0 and a == nums[i - 1]:
                continue

            l, r = i + 1, len(nums) - 1
            while l < r:
                threeSum = a + nums[l] + nums[r]
                if threeSum > 0:
                    r -= 1
                elif threeSum < 0:
                    l += 1
                else:
                    res.append([a, nums[l], nums[r]])
                    l += 1
                    r -= 1
                    while nums[l] == nums[l - 1] and l < r:
                        l += 1

        return res 
```
#### [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
```python
class Solution:
    def maxArea(self, heights: List[int]) -> int:
        res = 0

		# Brute force [T-O(n^2), S-O(1)]
		for i in range(len(heights)):
            for j in range(i + 1, len(heights)):
                res = max(res, min(heights[i], heights[j]) * (j - i))
        return res

		# Two pointers [T-O(n), S-O(1)]
		l, r = 0, len(heights) - 1

		while l < r:
            area = min(heights[l], heights[r]) * (r - l)
            res = max(res, area)
            if heights[l] <= heights[r]:
                l += 1
            else:
                r -= 1
        return res
```
#### [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)
```python
class Solution:
    def trap(self, height: List[int]) -> int:
        if not height:
            return 0
        n = len(height)
        res = 0

		# Brute Force O(n2), O(1)
		for i in range(n):
            leftMax = rightMax = height[i]

            for j in range(i):
                leftMax = max(leftMax, height[j])
            for j in range(i + 1, n):
                rightMax = max(rightMax, height[j])
                
            res += min(leftMax, rightMax) - height[i]
        return res
		
		# Prefix & Suffix Arrays O(n), O(n)
		leftMax = [0] * n
        rightMax = [0] * n
        
        leftMax[0] = height[0]
        for i in range(1, n):
            leftMax[i] = max(leftMax[i - 1], height[i])
        
        rightMax[n - 1] = height[n - 1]
        for i in range(n - 2, -1, -1):
            rightMax[i] = max(rightMax[i + 1], height[i])
        
        for i in range(n):
            res += min(leftMax[i], rightMax[i]) - height[i]
        return res

		# Stack O(n), O(n) ignored
		stack = []
			
		for i in range(len(height)):
            while stack and height[i] >= height[stack[-1]]:
                mid = height[stack.pop()]
                if stack:
                    right = height[i]
                    left = height[stack[-1]]
                    h = min(right, left) - mid
                    w = i - stack[-1] - 1
                    res += h * w
            stack.append(i)
        return res
	
		# Two Pointers O(n) O(1)
		l, r = 0, len(height) - 1
        leftMax, rightMax = height[l], height[r]
	
		while l < r:
            if leftMax < rightMax:
                l += 1
                leftMax = max(leftMax, height[l])
                res += leftMax - height[l]
            else:
                r -= 1
                rightMax = max(rightMax, height[r])
                res += rightMax - height[r]
        return res
```
# Sliding Window & Two pointer

- https://leetcode.com/problems/longest-substring-without-repeating-characters/
    
    ```cpp
    int solve(string str) {
      if(str.size() == 0) return 0;
      int maxans = INT_MIN;
      
      // brute force O(n^2) O(n)
      for (int i = 0; i < str.length(); i++) {
        unordered_set<int> set;
        for (int j = i; j < str.length(); j++) {
          if (set.find(str[j]) != set.end()) {
            maxans = max(maxans, j - i);
            break;
          }
          set.insert(str[j]);
        }
      }
      
      // optimized 1 O(2*n) O(n)
      int l = 0;
      for (int r = 0; r < str.length(); r++) {
        if (set.find(str[r]) != set.end()) {
          while (l < r && set.find(str[r]) != set.end()) {
            set.erase(str[l]);
            l++;
          }
        }
        set.insert(str[r]);
        maxans = max(maxans, r - l + 1);
      }
      return maxans;
    }
    ```
    
- https://leetcode.com/problems/max-consecutive-ones-iii/
    
    ```cpp
    // O(n) O(1)
    int longestOnes(vector<int>& nums, int k) {
        int n = nums.size();
        int l = 0, r = 0, len = 0, zeroCount = 0;
    
        while (r < n) {
            if (nums[r] == 0) zeroCount++;
            if (zeroCount > k) {
                if (nums[l] == 0) zeroCount--;
                l++;
            }
            if (zeroCount <= k) {
                len = max(len, r-l+1);
            } 
            r++;
        }
    
        return len;
    }
    ```
    
- https://leetcode.com/problems/fruit-into-baskets/
    
    ```cpp
    // O(n) O(n)
    int totalFruit(vector<int>& fruits) {
        int n = fruits.size();
        int len = 0, l = 0, r = 0;
        map<int, int> m;
    
        while (r < n) {
            m[fruits[r]]++;
            if (m.size() > 2) {
                m[fruits[l]]--;
                if (m[fruits[l]] == 0) m.erase(fruits[l]);
                l++;                
            }            
            if (m.size() <= 2) 
                len = max(len, r-l+1);
            r++;
        }
    
        return len;
    }
    ```
    
- https://leetcode.com/problems/longest-repeating-character-replacement/
    
    ```cpp
    // O(n) O(n)
    int characterReplacement(string s, int k) {
        int n = s.length();
        int c[26] = {0};
        int len = 0, maxFreq = 0, l = 0, r = 0;
    
        while (r < n) {
            c[s[r] - 'A']++;
            maxFreq = max(maxFreq, c[s[r] - 'A']);
            int changeCount = (r - l + 1) - maxFreq;
    
            if (changeCount > k) {
                c[s[l] - 'A']--;
                l++;
            } else {
                len = max(len, r - l + 1);
            }
            r++;
        }
        return len;
    }
    ```
    
- https://leetcode.com/problems/binary-subarrays-with-sum/
    
    ```cpp
    // O(n) O(1)
    int numSubarraysWithLessEqualSum (vector<int>& nums, int goal) {
        if (goal < 0) return 0;
        int n = nums.size();
        int count = 0, sum = 0, l = 0, r = 0; 
    
        while (r < n) {
            sum += nums[r];
    
            while (sum > goal) {
                sum -= nums[l];
                l++;
            }
            count += r-l+1;
            r++;
        }
        return count;
    }
    
    int numSubarraysWithSum(vector<int>& nums, int goal) {
        return numSubarraysWithLessEqualSum(nums, goal) - numSubarraysWithLessEqualSum(nums, goal-1);
    }
    ```
    
- https://leetcode.com/problems/count-number-of-nice-subarrays/
    
    ```cpp
    // O(n) O(1)
    int numberOfSubarraysLessEqualK(vector<int>& nums, int k) {
        if (k < 0) return 0;
        int n = nums.size();
        int count = 0, oddCount = 0, l = 0, r = 0;
    
        while (r < n) {
            oddCount += nums[r] % 2;
    
            while (oddCount > k) {
                oddCount -= (nums[l] % 2);
                l++;
            }
            count += r - l + 1;
            r++;
        }
        return count;
    }
    int numberOfSubarrays(vector<int>& nums, int k) {
        return numberOfSubarraysLessEqualK(nums, k) -
               numberOfSubarraysLessEqualK(nums, k - 1);
    }
    ```
    
- https://leetcode.com/problems/number-of-substrings-containing-all-three-characters/
    
    ```cpp
    // O(n) O(1)
    int numberOfSubstrings(string s) {
        int n = s.length(), count = 0;
        int lastChar[3] = {-1, -1, -1};
    
        for (int i=0; i<n; i++) {
            lastChar[s[i]-'a'] = i;
    
            if (lastChar[0] != -1 && lastChar[1] != -1 && lastChar[2] != -1) {
                count += min({lastChar[0], lastChar[1], lastChar[2]}) + 1;
            }
        }
        return count;
    }
    ```
    
- https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/
    
    ```cpp
    int maxScore(vector<int>& cardPoints, int k) {
        int n = cardPoints.size();
        int sum = 0;
        for (int i=0; i<k; i++) 
            sum += cardPoints[i];
        int maxSum = sum;
        
        for (int l=k-1, r=n-1; l>=0; ) {
            sum -= cardPoints[l];
            l--;
            sum += cardPoints[r];
            r--;
            maxSum = max(maxSum, sum);
        }
        return maxSum;
    }
    ```
    
- [Longest Substring with K Uniques](https://www.geeksforgeeks.org/problems/longest-k-unique-characters-substring0853/1)
    
    ```cpp
    int longestKSubstr(string &s, int k) {
    		// brute force O(n^2) O(1)
    		int ans = -1;  
        unordered_set<char> st;  
    
    		
        for (int i = 0; i < s.size(); i++) {
            st.clear();  
            for (int j = i; j < s.size(); j++) {
                st.insert(s[j]); 
                if (st.size() == k) 
                    ans = max(ans, j - i + 1);
                if(st.size() > k) break;
            }
        }
        return ans;
    		
    		// O(n) O(1)
        int n = s.size();
        int i = 0, j = 0;         
        int cnt = 0;               
        int maxi = -1;            
        vector<int> fre(26, 0);  
    
        while (j < n) {
            fre[s[j] - 'a']++; 
            if (fre[s[j] - 'a'] == 1) cnt++;
            
            while (cnt > k) {
                fre[s[i] - 'a']--;
                if (fre[s[i] - 'a'] == 0) cnt--;  
                i++;
            }
    
            if (cnt == k) 
                maxi = max(maxi, j - i + 1);
    
            j++;
        }
    
        return maxi;
    }
    ```
    
- https://leetcode.com/problems/subarrays-with-k-different-integers/
    
    ```cpp
    // O(n) O(1)
    int helper(vector<int>& nums, int k) {
        int n = nums.size();
        int count = 0, l = 0, r = 0;
        map<int, int> m;
    
        while (r < n) {
            m[nums[r]]++;
            while (m.size() > k) {
                m[nums[l]]--;
                if (m[nums[l]] == 0) 
                    m.erase(nums[l]);
                l++;
            }
            count += r-l+1;
            r++;
        }
        return count;
    }
    
    int subarraysWithKDistinct(vector<int>& nums, int k) {
        return helper(nums, k) - helper(nums, k-1);
    }
    ```
    
- https://leetcode.com/problems/minimum-window-substring/
    
    ```cpp
    // brute force O(n^2) O(1)
    1. generate all substring and compare with t string
    
    // two pointer O(n) O(1)
    string minWindow(string s, string t) {
        int len = 1e7, sIndex = -1, l = 0, r = 0, count = 0;
        int n = s.length();
        int m = t.length();
        map<char, int> mp;
    
        for (auto c: t) mp[c]++;
    
        while (r < n) {
            if (mp[s[r]] > 0) count++;
            mp[s[r]]--;
    
            while (count == m) {
                if (r-l+1 < len) {
                    len = min(r-l+1, len);
                    sIndex = l;
                }
                mp[s[l]]++;
                if (mp[s[l]] > 0) count--;
                l++;
            }
            r++;
        }        
        
         return sIndex == -1 ? "" : s.substr(sIndex, len);
    }
    ```
    
- https://leetcode.com/problems/trapping-rain-water/
    
    ```cpp
    int trap(vector<int> & arr) {
      int n = arr.size();
      int waterTrapped = 0;
      
      // brute force O(n^2) O(1)
      for (int i = 0; i < n; i++) {
        int j = i;
        int leftMax = 0, rightMax = 0;
        while (j >= 0) {
          leftMax = max(leftMax, arr[j]);
          j--;
        }
        
        j = i;
        while (j < n) {
          rightMax = max(rightMax, arr[j]);
          j++;
        }
        
        waterTrapped += min(leftMax, rightMax) - arr[i];
      }
      
      // better O(n) O(n)
      int prefix[n], suffix[n];
      prefix[0] = arr[0];
      
      for (int i = 1; i < n; i++) 
        prefix[i] = max(prefix[i - 1], arr[i]);
      
      suffix[n - 1] = arr[n - 1];
      for (int i = n - 2; i >= 0; i--) 
        suffix[i] = max(suffix[i + 1], arr[i]);
      
      for (int i = 0; i < n; i++) 
        waterTrapped += min(prefix[i], suffix[i]) - arr[i];
      
      // optimal O(n) O(1)
      int left = 0, right = n - 1;
      int maxLeft = 0, maxRight = 0;
      while (left <= right) {
        if (arr[left] <= arr[right]) {
          if (arr[left] >= maxLeft) {
            maxLeft = arr[left];
          } else {
            waterTrapped += maxLeft - arr[left];
          }
          left++;
        } else {
          if (arr[right] >= maxRight) {
            maxRight = arr[right];
          } else {
            waterTrapped += maxRight - arr[right];
          }
          right--;
        }
      }
      return waterTrapped;
    }
    ```
    
# Prefix / Suffix   
### prefix sum  
```python
class PrefixSum:
    def __init__(self, nums):
        self.prefix = []
        total = 0
        for n in nums:
            total += n
            self.prefix.append(total)
        
    def rangeSum(self, left, right):
        preRight = self.prefix[right]
        preLeft = self.prefix[left - 1] if left > 0 else 0
        return (preRight - preLeft)
```
### [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
	# Brute force [T-O(n^2), S-O(n)]
	n = len(nums)
        res = [0] * n

        for i in range(n):
            prod = 1
            for j in range(n):
                if i == j:
                    continue    
                prod *= nums[j]

            res[i] = prod
        return res

	# Division [T-O(n), S-O(n)]
	prod, zero_cnt = 1, 0
        for num in nums:
            if num:
                prod *= num
            else:
                zero_cnt +=  1
        if zero_cnt > 1: return [0] * len(nums)

        res = [0] * len(nums)
        for i, c in enumerate(nums):
            if zero_cnt: res[i] = 0 if c else prod
            else: res[i] = prod // c
        return res

	# prefix sum [T-O(n), S-O(n)]
	n = len(nums)
        res = [0] * n
        pref = [0] * n
        suff = [0] * n

        pref[0] = suff[n - 1] = 1
        for i in range(1, n):
            pref[i] = nums[i - 1] * pref[i - 1]
        for i in range(n - 2, -1, -1):
            suff[i] = nums[i + 1] * suff[i + 1]
        for i in range(n):
            res[i] = pref[i] * suff[i] 
        return res

	# Prefix & Suffix (Optimal) [T-O(n), S-O(n)]
	res = [1] * (len(nums))

        prefix = 1
        for i in range(len(nums)):
            res[i] = prefix
            prefix *= nums[i]
        postfix = 1
        for i in range(len(nums) - 1, -1, -1):
            res[i] *= postfix
            postfix *= nums[i]
        return res 
```
### Longest palindromic substring
```python
# Time: O(n^2), Space: O(n)
def longest(s):
    length = 0
    for i in range(len(s)):
        # odd length
        length = max(length, helper(s, i, i))
        
        # even length
        length = max(length, helper(s, i, i + 1)) 
    return length

def helper(s, l, r):
    maxLength = 0
    while l >= 0 and r < len(s) and s[l] == s[r]:
        if (r - l + 1) > maxLength:
            maxLength = r - l + 1
        l -= 1
        r += 1
    return maxLength
```
# Greedy

- https://leetcode.com/problems/assign-cookies/
    
    ```cpp
    // O(N logN + M logM + M) O(1)
    int findContentChildren(vector<int>& greed, vector<int>& cookieSize) {
        int n = greed.size();
        int m = cookieSize.size();
        sort(greed.begin(), greed.end());
        sort(cookieSize.begin(), cookieSize.end());
        int l = 0;
        int r = 0;
    
        while (l < m && r < n) {
            if (greed[r] <= cookieSize[l]) 
                r++;
            l++;
        }
    
        return r;
    }
    ```
    
- [Fractional Knapsack Problem](https://takeuforward.org/data-structure/fractional-knapsack-problem-greedy-approach/)
    
    ```cpp
    // O(n log n + n) O(1)
    bool static comp(Item a, Item b) {
       double r1 = (double) a.value / (double) a.weight;
       double r2 = (double) b.value / (double) b.weight;
       return r1 > r2;
    }
    
    double fractionalKnapsack(int W, Item arr[], int n) { 
    	// arr = { {100,20},{60,10},{120,30} };
      sort(arr, arr + n, comp);
      int curWeight = 0;
      double finalvalue = 0.0;
    
      for (int i = 0; i < n; i++) {
         if (curWeight + arr[i].weight <= W) {
            curWeight += arr[i].weight;
            finalvalue += arr[i].value;
         } else {
            int remain = W - curWeight;
            finalvalue += (arr[i].value / (double) arr[i].weight) * (double) remain;
            break;
         }
      }
    
      return finalvalue;
    }
    ```
    
- [Greedy algorithm to find minimum number of coins](https://takeuforward.org/data-structure/find-minimum-number-of-coins/)
    
    ```cpp
    // O(V) O(1)
    int main() {
      int V = 49;
      vector < int > ans;
      int coins[] = {1, 2, 5, 10, 20, 50, 100, 500, 1000};
      int n = 9;
      for (int i = n - 1; i >= 0; i--) {
        while (V >= coins[i]) {
          V -= coins[i];
          ans.push_back(coins[i]);
        }
      }
      cout<<"The minimum number of coins is "<<ans.size()<<endl;
      cout<<"The coins are "<<endl;
      for (int i = 0; i < ans.size(); i++) {
        cout << ans[i] << " ";
      }
    ```
    
- https://leetcode.com/problems/lemonade-change/
    
    ```cpp
    // O(n) O(1)
    bool lemonadeChange(vector<int>& bills) {
        int five = 0; 
        int ten = 0;   
    
        for(int i = 0; i < bills.size(); i++){
            if(bills[i] == 5)
                five++;  
            else if(bills[i] == 10){
                if(five){
                    five--; 
                    ten++;   
                } else return false;  
            } else {
                if(five && ten){
                    five--; 
                    ten--;   
                } else if (five >= 3)
                    five -= 3;  
                else return false;  
            }
        }  
        return true;  
    }
    ```
    
- https://leetcode.com/problems/valid-parenthesis-string/
- [N meetings in one room](https://takeuforward.org/data-structure/n-meetings-in-one-room/)
    
    ![image.png](image%208.png)
    
    ```cpp
    // O(n log n) O(n)
    struct meeting {
       int start;
       int end;
       int pos;
    };
    
    bool static comparator(struct meeting m1, struct meeting m2) {
       if (m1.end < m2.end) return true;
       else if (m1.end > m2.end) return false;
       else if (m1.pos < m2.pos) return true;
       return false;
    }
    
    void maxMeetings(int s[], int e[], int n) {
      struct meeting meet[n];
      for (int i = 0; i < n; i++) {
         meet[i].start = s[i], meet[i].end = e[i], meet[i].pos = i + 1;
      }
    
      sort(meet, meet + n, comparator);
      vector<int> answer;
    
      int limit = meet[0].end;
      answer.push_back(meet[0].pos);
    
      for (int i = 1; i < n; i++) {
         if (meet[i].start > limit) {
            limit = meet[i].end;
            answer.push_back(meet[i].pos);
         }
      }
      
      cout<<"The order in which the meetings will be performed is "<<endl;
      for (int i = 0; i < answer.size(); i++) {
         cout << answer[i] << " ";
      }
    }
    
    ```
    
- https://leetcode.com/problems/jump-game/
    
    ```cpp
    // O(n) O(1)
    bool canJump(vector<int>& nums) {
        int maxIndex = 0;
        for(int i = 0; i < nums.size(); i++){
            if (i > maxIndex){
                return false;
            }
            maxIndex = max(maxIndex, i + nums[i]);
        }
        return true;
    }
    ```
    
- https://leetcode.com/problems/jump-game-ii/
    
    ```cpp
    int jump(vector<int>& nums) {
        int l = 0, r = 0, jumps = 0;
        while (r < nums.size() - 1) {
            int furthest = 0;
            for (int i=l; i<=r; i++) {
                furthest = max(furthest, i+nums[i]);
            }
            l = r + 1;
            r = furthest;
            jumps++;
        }
        return jumps;
    }
    ```
    
- [Minimum number of platforms required for a railway](https://takeuforward.org/data-structure/minimum-number-of-platforms-required-for-a-railway/)
    
    ![image.png](image%209.png)
    
    ```cpp
    // brute force O(n^2) O(1)
    int countPlatforms(int n,int arr[],int dep[]) {
        int ans=1; 
        
        for(int i=0; i<=n-1; i++) {
            int count=1; 
            for(int j=i+1; j<=n-1; j++) {
    					if((arr[i]>=arr[j] && arr[i]<=dep[j]) ||
    					   (arr[j]>=arr[i] && arr[j]<=dep[i])) {
    							count++;
    					}
            }
            ans=max(ans,count); 
        }
        return ans;
     }
     
     // sorting O(nlogn) O(1)
     int countPlatforms(int n,int arr[],int dep[]) {
        sort(arr,arr+n);
        sort(dep,dep+n);
        int ans=1;
        int count=1;
        int i=1,j=0;
        
        while(i<n && j<n)
        {
            if(arr[i] <= dep[j]) {
                count++;
                i++;
            } else {
                count--;
                j++;
            }
            ans=max(ans,count); 
        }
        return ans;
     }
    ```
    
- [Job sequencing Problem](https://takeuforward.org/data-structure/job-sequencing-problem/)
    
    ```cpp
    // O(N log N) + O(N*M) O(M)
    struct Job {
       int id; // Job Id 
       int dead; // Deadline of job 
       int profit; // Profit if job is over before or on deadline 
    };
    
    class Solution {
       public:
          bool static comparison(Job a, Job b) {
             return (a.profit > b.profit);
          }
    
       pair<int, int> JobScheduling(Job arr[], int n) {
          sort(arr, arr + n, comparison);
          int maxi = arr[0].dead;
          for (int i = 1; i < n; i++) {
             maxi = max(maxi, arr[i].dead);
          }
    
          int slot[maxi + 1];
    
          for (int i = 0; i <= maxi; i++)
             slot[i] = -1;
    
          int countJobs = 0, jobProfit = 0;
    
          for (int i = 0; i < n; i++) {
             for (int j = arr[i].dead; j > 0; j--) {
                if (slot[j] == -1) {
                   slot[j] = i;
                   countJobs++;
                   jobProfit += arr[i].profit;
                   break;
                }
             }
          }
          return make_pair(countJobs, jobProfit);
       }
    };
    
    int main() {
       int n = 4;
       Job arr[n] = {{1,4,20},{2,1,10},{3,2,40},{4,2,30}};
    
       Solution ob;
       //function call
       pair < int, int > ans = ob.JobScheduling(arr, n);
       cout << ans.first << " " << ans.second << endl;
    
       return 0;
    } 
    ```
    
- https://leetcode.com/problems/candy/
    
    ```cpp
    // O(n) O(n)
    int candy(vector<int>& ratings) {
        vector<int> candies(ratings.size());
        for (int i = 0; i < candies.size(); i++) {
            candies[i] = 1;
        }
        
        for (int i= 1; i < ratings.size(); i++) {
            if (ratings[i] > ratings[i - 1]) {
                candies[i] = candies[i - 1] + 1;
            }
        }
    
        for (int i = ratings.size() - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1]) {
                candies[i] = max(candies[i], candies[i + 1] + 1);
            }
        }
        
        int total = 0;
        for (int i = 0; i < candies.size(); i++) {
            total += candies[i];
        }
        
        return total;
    }
    
    // optimal O(n) O(1)
    int candy(vector<int>& ratings) {
        int n = ratings.size();
        int candy = n, i=1;
        while(i<n){
            if(ratings[i] == ratings[i-1]){
                i++;
                continue;
            }
            
            int peak = 0;
            while(ratings[i] > ratings [i-1]){
                peak++;
                candy += peak;
                i++;
                if(i == n) return candy;
            }
            
            int valley = 0;
            while(i<n && ratings[i] < ratings[i-1]){
                valley++;
                candy += valley;
                i++;
            }
            candy -= min(peak, valley); 
        }
        return candy;
    }
    ```
    
- [Program for Shortest Job First (or SJF) CPU Schedling](https://takeuforward.org/Greedy/shortest-job-first-or-sjf-cpu-scheduling)
    
    ```cpp
    // O(N logN + N) O(1)
    float shortestJobFirst(vector<int> jobs) {
        sort(jobs.begin(), jobs.end()); 
        float waitTime = 0; 
        int totalTime = 0; 
        int n = jobs.size(); 
    
        for(int i = 0; i < n; ++i) {
            waitTime += totalTime; 
            totalTime += jobs[i]; 
        }
        return waitTime / n; 
    }
    ```
    
- https://leetcode.com/problems/insert-interval/
    
    ```cpp
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        int n = intervals.size(), i = 0;
        vector<vector<int>> res;
    
        while(i < n && intervals[i][1] < newInterval[0]){
            res.push_back(intervals[i]);
            i++;
        }                           
    
        while(i < n && newInterval[1] >= intervals[i][0]){
            newInterval[0] = min(newInterval[0], intervals[i][0]);
            newInterval[1] = max(newInterval[1], intervals[i][1]);
            i++;
        }
        res.push_back(newInterval);
     
        while(i < n){
            res.push_back(intervals[i]);
            i++;
        }
        return res;
    }
    ```
    
- https://leetcode.com/problems/merge-intervals/
    
    ```cpp
    vector<vector<int>> mergeOverlappingIntervals(vector<vector<int>> &arr) {
        int n = arr.size(); 
        sort(arr.begin(), arr.end());
        vector<vector<int>> ans;
    	
    		// O(N*logN) + O(2*N) O(N)
        for (int i = 0; i < n; i++) { 
            int start = arr[i][0];
            int end = arr[i][1];
            if (!ans.empty() && end <= ans.back()[1]) {
                continue;
            }
    
            for (int j = i + 1; j < n; j++) {
                if (arr[j][0] <= end) {
                    end = max(end, arr[j][1]);
                }
                else {
                    break;
                }
            }
            ans.push_back({start, end});
        }
        
        // O(N*logN) + O(N) O(N)
    	  for (int i = 0; i < n; i++) {
            if (ans.empty() || arr[i][0] > ans.back()[1]) {
                ans.push_back(arr[i]);
            }
            else {
                ans.back()[1] = max(ans.back()[1], arr[i][1]);
            }
        }
        return ans;
    }
    ```
    
- https://leetcode.com/problems/non-overlapping-intervals/
    
    ```cpp
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());
        int ans = 0;
        int prevEnd = intervals[0][1];
        
        for (int i=1; i<intervals.size(); i++) {
            int start = intervals[i][0];
            int end = intervals[i][1];
            
            if (start >= prevEnd) 
                prevEnd = end;
            else {
                ans++;
                prevEnd = min(end, prevEnd);
            }
        }
        return ans;
    }
    ```
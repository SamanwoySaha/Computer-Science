---
title: Sorting
draft: false
tags: 
date: 19-Aug-2025
---
# Selection Sort
    
```cpp
// select minimum
// swap with current position
// O(n^2) O(1)
for (int i = 0; i < n - 1; i++) {
	int mini = i;
	for (int j = i + 1; j < n; j++) {
		if (arr[j] < arr[mini])
			mini = j;
	}
	swap(arr[mini], arr[i]);
}

```
# Bubble Sort
```cpp
// swap two adjacent element if a[j] > a[j+1]
// worst: O(n^2) best: O(n) (if sorted array)  O(1)
for (int i = n - 1; i >= 0; i--) {
	int isSwapped = 0;
	for (int j = 0; j <= i - 1; j++) {
		if (arr[j] > arr[j + 1]) {
			swap(arr[j], arr[j+1]);
			isSwapped = 1;
		}
	}
	if (isSwapped) break;
}

```
# Insertion Sort
```cpp
// Take element and place it in it's correct position
// worst: O(n^2) O(1) best: O(n) (if sorted array)  O(1)
for (int i = 0; i <= n - 1; i++) {
	int j = i;
	while (j > 0 && arr[j - 1] > arr[j]) {
		swap(a[j-1], a[j]);
		j--;
	}
}

```

```python
# Python implementation of Insertion Sort
def insertionSort(arr):
	# Traverse through 1 to len(arr)
    for i in range(1, len(arr)):
        j = i - 1
        while j >= 0 and arr[j + 1] < arr[j]:
            # arr[j] and arr[j + 1] are out of order so swap them 
            tmp = arr[j + 1]
            arr[j + 1] = arr[j]
            arr[j] = tmp
            j -= 1
    return arr
    
# tc - O(n^2)
# unstable   
```
    
# Merge Sort
    
```cpp
// O(nlogn)  O(1)
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

void mergeSort(vector<int> &arr, int low, int high) {
	if (low >= high) return;
	int mid = (low + high) / 2 ;
	mergeSort(arr, low, mid);  // left half
	mergeSort(arr, mid + 1, high); // right half
	merge(arr, low, mid, high);  // merging sorted halves
}

```

```python
# Implementation of MergeSort
def mergeSort(arr, s, e):
    if e - s + 1 <= 1:
        return arr

    # The middle index of the array
    m = (s + e) // 2

    # Sort the left half
    mergeSort(arr, s, m)

    # Sort the right half
    mergeSort(arr, m + 1, e)

    # Merge sorted halfs
    merge(arr, s, m, e)
    
    return arr

# Merge in-place
def merge(arr, s, m, e):
    # Copy the sorted left & right halfs to temp arrays
    L = arr[s: m + 1]
    R = arr[m + 1: e + 1]

    i = 0 # index for L
    j = 0 # index for R
    k = s # index for arr

    # Merge the two sorted halfs into the original array
    while i < len(L) and j < len(R):
        if L[i] <= R[j]:
            arr[k] = L[i]
            i += 1
        else:
            arr[k] = R[j]
            j += 1
        k += 1

    # One of the halfs will have elements remaining
    while i < len(L):
        arr[k] = L[i]
        i += 1
        k += 1
    while j < len(R):
        arr[k] = R[j]
        j += 1
        k += 1
        
# tc - O(nlogn)
# stable   
```
    
# Quick Sort
    
```cpp
// best and avg: O(nlogn) O(1) (pivot is middle or near to middle element)
// worst: O(n^2) O(1) (pivot is greatest or smallest)
int partition(vector<int> &arr, int low, int high) {
	int pivot = arr[low];
	int i = low;
	int j = high;

	while (i < j) {
		while (arr[i] <= pivot && i <= high - 1)
			i++;

		while (arr[j] > pivot && j >= low + 1)
			j--;

		if (i < j) swap(arr[i], arr[j]);
	}
	swap(arr[low], arr[j]);
	return j;
}

void qs(vector<int> &arr, int low, int high) {
	if (low < high) {
		int pIndex = partition(arr, low, high);
		qs(arr, low, pIndex - 1);
		qs(arr, pIndex + 1, high);
	}
}

```

```python
# Implementation of QuickSort
def quickSort(arr, s, e):
    if e - s + 1 <= 1:
        return

    pivot = arr[e]
    left = s # pointer for left side

    # Partition: elements smaller than pivot on left side
    for i in range(s, e):
        if arr[i] < pivot:
            tmp = arr[left]
            arr[left] = arr[i]
            arr[i] = tmp
            left += 1

    # Move pivot in-between left & right sides
    arr[e] = arr[left]
    arr[left] = pivot
    
    # Quick sort left side
    quickSort(arr, s, left - 1)

    # Quick sort right side
    quickSort(arr, left + 1, e)

    return arr
    
# tc - O(nlogn)
# unstable  
```

# Bucket Sort   
```python
def bucketSort(arr):
    # Assuming arr only contains 0, 1 or 2
    counts = [0, 0, 0]

    # Count the quantity of each val in arr
    for n in arr:
        counts[n] += 1
    
    # Fill each bucket in the original array
    i = 0
    for n in range(len(counts)):
        for j in range(counts[n]):
            arr[i] = n
            i += 1
    return arr
    
# tc - O(n)
# unstable 
```
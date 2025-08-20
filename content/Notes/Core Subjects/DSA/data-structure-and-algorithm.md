---
title: data-structure-and-algorithm
draft: true
tags: 
date: 19-Aug-2025
---
# Data Structure and Algorithm   
# Array   
## Binary Search   
### Basic   

> 33. Search in Rotated Sorted Array   

```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
		# Brute Force O(n) O(1)
        for i in range(len(nums)):
            if nums[i] == target:
                return i
        return -1

		# Binary Search O(logn) O(1) ignored
		l, r = 0, len(nums) - 1

        while l < r:
            m = (l + r) // 2
            if nums[m] > nums[r]:
                l = m + 1
            else:
                r = m

        pivot = l
        
        def binary_search(left: int, right: int) -> int:
            while left <= right:
                mid = (left + right) // 2
                if nums[mid] == target:
                    return mid
                elif nums[mid] < target:
                    left = mid + 1
                else:
                    right = mid - 1
            return -1

        result = binary_search(0, pivot - 1)
        if result != -1:
            return result
        
        return binary_search(pivot, len(nums) - 1)
	
		# Binary Search (Two Pass) O(logn) O(1) ignored
		l, r = 0, len(nums) - 1

        while l < r:
            m = (l + r) // 2
            if nums[m] > nums[r]:
                l = m + 1
            else:
                r = m

        pivot = l
        l, r = 0, len(nums) - 1

        if target >= nums[pivot] and target <= nums[r]:
            l = pivot
        else:
            r = pivot - 1

        while l <= r:
            m = (l + r) // 2
            if nums[m] == target:
                return m
            elif nums[m] < target:
                l = m + 1
            else:
                r = m - 1

        return -1
		
		# binary search (One pass) O(logn) O(1)
		l, r = 0, len(nums) - 1

        while l <= r:
            mid = (l + r) // 2
            if target == nums[mid]:
                return mid

            if nums[l] <= nums[mid]:
                if target > nums[mid] or target < nums[l]:
                    l = mid + 1
                else:
                    r = mid - 1
                    
            else:
                if target < nums[mid] or target > nums[r]:
                    r = mid - 1
                else:
                    l = mid + 1
        return -1
		

```
> 4. Median of Two Sorted Arrays   

```
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
		# Brute Force O((n+m)log⁡(n+m)) O(n+m)
        len1 = len(nums1)
        len2 = len(nums2)
        merged = nums1 + nums2
        merged.sort()
        
        totalLen = len(merged)
        if totalLen % 2 == 0:
            return (merged[totalLen // 2 - 1] + merged[totalLen // 2]) / 2.0
        else:
            return merged[totalLen // 2]

		# Two Pointers O(n+m) O(1)
		len1, len2 = len(nums1), len(nums2)
        i = j = 0
        median1 = median2 = 0

        for count in range((len1 + len2) // 2 + 1):
            median2 = median1
            if i < len1 and j < len2:
                if nums1[i] > nums2[j]:
                    median1 = nums2[j]
                    j += 1
                else:
                    median1 = nums1[i]
                    i += 1
            elif i < len1:
                median1 = nums1[i]
                i += 1
            else:
                median1 = nums2[j]
                j += 1

        if (len1 + len2) % 2 == 1:
            return float(median1)
        else:
            return (median1 + median2) / 2.0

		# Binary Search (optimal) O(log(min(n,m))) O(1)
		A, B = nums1, nums2
        total = len(nums1) + len(nums2)
        half = total // 2

        if len(B) < len(A):
            A, B = B, A

        l, r = 0, len(A) - 1
        while True:
            i = (l + r) // 2
            j = half - i - 2

            Aleft = A[i] if i >= 0 else float("-infinity")
            Aright = A[i + 1] if (i + 1) < len(A) else float("infinity")
            Bleft = B[j] if j >= 0 else float("-infinity")
            Bright = B[j + 1] if (j + 1) < len(B) else float("infinity")

            if Aleft <= Bright and Bleft <= Aright:
                if total % 2:
                    return min(Aright, Bright)
                return (max(Aleft, Bleft) + min(Aright, Bright)) / 2
            elif Aleft > Bright:
                r = i - 1
            else:
                l = i + 1

# binary search O(log(m+n)) O(log(m+n)) ignored
class Solution:
    def get_kth(self, a: List[int], m: int, b: List[int], n: int, k: int, a_start: int = 0, b_start: int = 0) -> int:
        if m > n:
            return self.get_kth(b, n, a, m, k, b_start, a_start)
        if m == 0:
            return b[b_start + k - 1]
        if k == 1:
            return min(a[a_start], b[b_start])
        
        i = min(m, k // 2)
        j = min(n, k // 2)
        
        if a[a_start + i - 1] > b[b_start + j - 1]:
            return self.get_kth(a, m, b, n - j, k - j, a_start, b_start + j)
        else:
            return self.get_kth(a, m - i, b, n, k - i, a_start + i, b_start)
    
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        left = (len(nums1) + len(nums2) + 1) // 2
        right = (len(nums1) + len(nums2) + 2) // 2
        return (self.get_kth(nums1, len(nums1), nums2, len(nums2), left) +
                self.get_kth(nums1, len(nums1), nums2, len(nums2), right)) / 2.0

```
### Binary Search on range of values   
> Binary Search on range of values   

```
# low = 1, high = 100

# Binary search on some range of values
def binarySearch(low, high):

    while low <= high:
        mid = (low + high) // 2

        if isCorrect(mid) > 0:
            high = mid - 1
        elif isCorrect(mid) < 0:
            low = mid + 1
        else:
            return mid
    return -1

# Return 1 if n is too big, -1 if too small, 0 if correct
def isCorrect(n):
    if n > 10:
        return 1
    elif n < 10:
        return -1
    else:
        return 0
        
# tc - O(nlogn)  
```
> 875. Koko Eating Bananas   

```
class Solution:
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
		# Brute Force O(m∗n) O(1)
        speed = 1
        while True:
            totalTime = 0
            for pile in piles:
                totalTime += math.ceil(pile / speed)
            
            if totalTime <= h:
                return speed
            speed += 1
        return speed

		# Binary Search O(n∗logm) O(1)
		l, r = 1, max(piles)
        res = r

        while l <= r:
            k = (l + r) // 2

            totalTime = 0
            for p in piles:
                totalTime += math.ceil(float(p) / k)
            if totalTime <= h:
                res = k
                r = k - 1
            else:
                l = k + 1
        return res

```
### Upperbound   
> upperbound   

```
	# Upper Bound O(logn) O(1)
	def search(self, nums: List[int], target: int) -> int:
		l, r = 0, len(nums)

        while l < r:
            m = l + ((r - l) // 2)  
            if nums[m] > target:
                r = m
            elif nums[m] <= target:
                l = m + 1
        return l - 1 if (l and nums[l - 1] == target) else -1
```
> 981. Time Based Key-Value Store   

```
# Brute Force T- O(1) for set() and O(n) for get() S- O(m*n)
class TimeMap:
    def __init__(self):
        self.keyStore = {}

    def set(self, key: str, value: str, timestamp: int) -> None:
        if key not in self.keyStore:
            self.keyStore[key] = {}
        if timestamp not in self.keyStore[key]:
            self.keyStore[key][timestamp] = []
        self.keyStore[key][timestamp].append(value)

    def get(self, key: str, timestamp: int) -> str:
        if key not in self.keyStore:
            return ""
        seen = 0

        for time in self.keyStore[key]:
            if time <= timestamp:
                seen = max(seen, time)
        return "" if seen == 0 else self.keyStore[key][seen][-1]

# Binary Search (Sorted Map) T- O(1) for set() and O(logn) for get() S- O(m*n) ignored
from sortedcontainers import SortedDict

class TimeMap:
    def __init__(self):
        self.m = defaultdict(SortedDict)

    def set(self, key: str, value: str, timestamp: int) -> None:
        self.m[key][timestamp] = value

    def get(self, key: str, timestamp: int) -> str:
        if key not in self.m:
            return ""
        
        timestamps = self.m[key]
        idx = timestamps.bisect_right(timestamp) - 1
        
        if idx >= 0:
            closest_time = timestamps.iloc[idx]
            return timestamps[closest_time]
        return ""

# Binary Search (Array) T- O(1) for set() and O(logn) for get() S- O(m*n)
class TimeMap:
    def __init__(self):
        self.keyStore = {}  # key : list of [val, timestamp]

    def set(self, key: str, value: str, timestamp: int) -> None:
        if key not in self.keyStore:
            self.keyStore[key] = []
        self.keyStore[key].append([value, timestamp])

    def get(self, key: str, timestamp: int) -> str:
        res, values = "", self.keyStore.get(key, [])
        l, r = 0, len(values) - 1
        while l <= r:
            m = (l + r) // 2
            if values[m][1] <= timestamp:
                res = values[m][0]
                l = m + 1
            else:
                r = m - 1
        return res

```
### Lowerbound   
> lowerbound   

```
	# Lower Bound O(logn) O(1)
	def search(self, nums: List[int], target: int) -> int:
		l, r = 0, len(nums)

        while l < r:
            m = l + ((r - l) // 2)  
            if nums[m] >= target:
                r = m
            elif nums[m] < target:
                l = m + 1
        return l if (l < len(nums) and nums[l] == target) else -1
```
> 153. Find Minimum in Rotated Sorted Array   

```
class Solution:
    def findMin(self, nums: List[int]) -> int:
		# brute force O(n) O(1)
        return min(nums)

		# Binary Search O(logn) O(1)
		res = nums[0]
        l, r = 0, len(nums) - 1

        while l <= r:
            if nums[l] < nums[r]:
                res = min(res, nums[l])
                break
            
            m = (l + r) // 2
            res = min(res, nums[m])
            if nums[m] >= nums[l]:
                l = m + 1
            else:
                r = m - 1
        return res

		# Binary Search (Lower Bound) O(logn) O(1)
		l, r = 0, len(nums) - 1

        while l < r:
            m = l + (r - l) // 2
            if nums[m] < nums[r]:
                r = m
            else:
                l = m + 1
        return nums[l]

```
## Problems   
> Encode and Decode Strings   

```
class Solution:
    # Brute force [T-O(m), S-O(m+n)]
    # Where mm is the sum of lengths of all the strings and nn is the number of strings.
    def encode(self, strs: List[str]) -> str:
        if not strs:
            return ""
        sizes, res = [], ""
        for s in strs:
            sizes.append(len(s))
        for sz in sizes:
            res += str(sz)
            res += ','
        res += '#'
        for s in strs:
            res += s
        return res

    def decode(self, s: str) -> List[str]:
        if not s:
            return []
        sizes, res, i = [], [], 0
        while s[i] != '#':
            cur = ""
            while s[i] != ',':
                cur += s[i]
                i += 1
            sizes.append(int(cur))
            i += 1
        i += 1
        for sz in sizes:
            res.append(s[i:i + sz])
            i += sz
        return res

    # Optimal [T-O(m), S-O(m+n)]
    def encode(self, strs: List[str]) -> str:
	if not strs:
            return ""
        res = ""
        for s in strs:
            res += str(len(s)) + "#" + s
        return res

    def decode(self, s: str) -> List[str]:
		if not s:
            return []
        res, i = [], 0

        while i < len(s):
            j = i
            while s[j] != '#':
                j += 1
            length = int(s[i:j])
            res.append(s[j+1 : j+1+length])
            i = j + 1 + length

        return res 
```
  
> 239. Sliding Window Maximum   

```
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        output = []

		# brute force O(n∗k) O(1) extra space, O(n−k+1) space for the output array.
        for i in range(len(nums) - k + 1):
            maxi = nums[i]
            for j in range(i, i + k):
                maxi = max(maxi, nums[j])
            output.append(maxi)

        return output

		# heap O(nlog⁡n) O(n) ignored
		heap = []

        for i in range(len(nums)):
            heapq.heappush(heap, (-nums[i], i))
            if i >= k - 1:
                while heap[0][1] <= i - k:
                    heapq.heappop(heap)
                output.append(-heap[0][0])
        return output

		# Dynamic Programming O(n) O(n) ignored
		n = len(nums)
        leftMax = [0] * n
        rightMax = [0] * n

        leftMax[0] = nums[0]
        rightMax[n - 1] = nums[n - 1]

        for i in range(1, n):
            if i % k == 0:
                leftMax[i] = nums[i]
            else:
                leftMax[i] = max(leftMax[i - 1], nums[i])

            if (n - 1 - i) % k == 0:
                rightMax[n - 1 - i] = nums[n - 1 - i]
            else:
                rightMax[n - 1 - i] = max(rightMax[n - i], nums[n - 1 - i])

        output = [0] * (n - k + 1)

        for i in range(n - k + 1):
            output[i] = max(leftMax[i + k - 1], rightMax[i])

        return output

		# deque O(n) O(n)
		q = deque()  # index
        l = r = 0

        while r < len(nums):
            while q and nums[q[-1]] < nums[r]:
                q.pop()
            q.append(r)

            if l > q[0]:
                q.popleft()

            if (r + 1) >= k:
                output.append(nums[q[0]])
                l += 1
            r += 1

        return output

# segment tree O(nlog⁡n) O(n) ignored
class SegmentTree:
    def __init__(self, N, A):
        self.n = N
        while (self.n & (self.n - 1)) != 0:
            self.n += 1
        self.build(N, A)

    def build(self, N, A):
        self.tree = [float('-inf')] * (2 * self.n)
        for i in range(N):
            self.tree[self.n + i] = A[i]
        for i in range(self.n - 1, 0, -1):
            self.tree[i] = max(self.tree[i << 1], self.tree[i << 1 | 1])

    def query(self, l, r):
        res = float('-inf')
        l += self.n
        r += self.n + 1
        while l < r:
            if l & 1:
                res = max(res, self.tree[l])
                l += 1
            if r & 1:
                r -= 1
                res = max(res, self.tree[r])
            l >>= 1
            r >>= 1
        return res


class Solution:
    def maxSlidingWindow(self, nums, k):
        n = len(nums)
        segTree = SegmentTree(n, nums)
        output = []
        for i in range(n - k + 1):
            output.append(segTree.query(i, i + k - 1))
        return output

```
  
> Find the middle of a linked list with two pointers   

```
# Time: O(n), Space: O(1)
def middleOfList(head):
    slow, fast = head, head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    return slow
```
> Determine if the linked list contains a cycle   

```
# Time: O(n), Space: O(1)
def hasCycle(head):
    slow, fast = head, head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False
```
> Determine if the linked list contains a cycle and return the beginning of the cycle, otherwise return null   

```
# Time: O(n), Space: O(1)
def cycleStart(head):
    slow, fast = head, head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            break

    if not fast or not fast.next:
        return None
    
    slow2 = head
    while slow != slow2:
        slow = slow.next
        slow2 = slow2.next
    return slow
```
# Recursion   

# Trees   
## Data Structure   
> Tree   

```
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None
```
> Binary Search Tree (BST)   

```
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None

def search(root, target):
    if not root:
        return False
    
    if target > root.val:
        return search(root.right, target)
    elif target < root.val:
        return search(root.left, target)
    else:
        return True
        
# Insert a new node and return the root of the BST.
def insert(root, val):
    if not root:
        return TreeNode(val)
    
    if val > root.val:
        root.right = insert(root.right, val)
    elif val < root.val:
        root.left = insert(root.left, val)
    return root

# Return the minimum value node of the BST.
def minValueNode(root):
    curr = root
    while curr and curr.left:
        curr = curr.left
    return curr

# Remove a node and return the root of the BST.
def remove(root, val):
    if not root:
        return None
    
    if val > root.val:
        root.right = remove(root.right, val)
    elif val < root.val:
        root.left = remove(root.left, val)
    else:
        if not root.left:
            return root.right
        elif not root.right:
            return root.left
        else:
            minNode = minValueNode(root.right)
            root.val = minNode.val
            root.right = remove(root.right, minNode.val)
    return root 
```
> Tree Traversal   

```
from collections import deque

class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None

# recursive
def inorder(root): # dfs
    if not root:
        return    
    inorder(root.left)
    print(root.val)
    inorder(root.right)

# iterative
# Time and space: O(n)
def inorder(root):
    stack = []
    curr = root

    while curr or stack:
        if curr:
            stack.append(curr)
            curr = curr.left
        else:
            curr = stack.pop()
            print(curr.val)
            curr = curr.right

# recursive
def preorder(root): # dfs
    if not root:
        return    
    print(root.val)
    preorder(root.left)
    preorder(root.right)

# iterative
# Time and space: O(n)
def preorder(root):
    stack = []
    curr = root
    while curr or stack:
        if curr:
            print(curr.val)
            if curr.right:
                stack.append(curr.right)
            curr = curr.left
        else:
            curr = stack.pop()

# recursive
def postorder(root): # dfs
    if not root:
        return    
    postorder(root.left)
    postorder(root.right)
    print(root.val)

# iterative
# Time and space: O(n)
def postorder(root):
    stack = [root]
    visit = [False]
    while stack:
        curr, visited = stack.pop(), visit.pop()
        if curr:
            if visited:
                print(curr.val)
            else:
                stack.append(curr)
                visit.append(True)
                stack.append(curr.right)
                visit.append(False)
                stack.append(curr.left)
                visit.append(False)

def bfs(root): # bfs (level order) 
    queue = deque()

    if root:
        queue.append(root)
    
    level = 0
    while len(queue) > 0:
        print("level: ", level)
        for i in range(len(queue)):
            curr = queue.popleft()
            print(curr.val)
            if curr.left:
                queue.append(curr.left)
            if curr.right:
                queue.append(curr.right)
        level += 1 
```
> BST Set   

```

```
> BST Map   

```
# Insert O(nlogn)
# Remove O(nlogn)
# Search O(nlogn)
# Inorder Traversal O(n) 
# Inorder Traversal O(n) 
# Inorder Traversal O(n) 
```
# Hashing   
## Problem   
> 217. Contains Duplicate   

```
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:

	# brute force [T-O(n^2), S-O(1)]
	for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                if nums[i] == nums[j]:
                    return True
        return False

	# Sorting [T-O(nlogn), S-O(1)]
	nums.sort()
        for i in range(1, len(nums)):
            if nums[i] == nums[i - 1]:
                return True2
        return False       

	# Hash Set [T-O(n), S-O(n)]
	seen = set()
        for num in nums:
            if num in seen:
                return True
            seen.add(num)
        return False

	# Hash Set Length [T-O(n), S-O(n)]
	return len(set(nums)) < len(nums 
```
> 242. Valid Anagram   

```
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
	if len(s) != len(t):
            return False

	# Sorting [T-O(nlogn + mlogm), S-O(1)]
        return sorted(s) == sorted(t)

	# Hash Map [T-O(n+m), S-O(1)]
	countS, countT = {}, {}
        for i in range(len(s)):
            countS[s[i]] = 1 + countS.get(s[i], 0)
            countT[t[i]] = 1 + countT.get(t[i], 0)
        return countS == countT

	# Hash Table (Using Array) [T-O(n+m), S-O(1)]
	count = [0] * 26
        for i in range(len(s)):
            count[ord(s[i]) - ord('a')] += 1 # ord() -> returns an integer representing that character's position in the Unicode table
            count[ord(t[i]) - ord('a')] -= 1

        for val in count:
            if val != 0:
                return False
        return True 
```
> Two Sum   

```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:

	# Brute Force [T-O(n^2), S-(1)]
	for i in range(len(nums)):
	    for j in range(i + 1, len(nums)):
	        if nums[i] + nums[j] == target:
	            return [i, j]
	return []

	# Sorting [T-O(nlogn), S-O(n)]
	A = []
        for i, num in enumerate(nums):
            A.append([num, i])

        A.sort()
        i, j = 0, len(nums) - 1
        while i < j:
            cur = A[i][0] + A[j][0]
            if cur == target:
                return [min(A[i][1], A[j][1]), 
                        max(A[i][1], A[j][1])]
            elif cur < target:
                i += 1
            else:
                j -= 1
        return []

	# Hash Map (Two Pass) [T-O(n), S-O(n)]
	indices = {}  # val -> index

        for i, n in enumerate(nums):
            indices[n] = i

        for i, n in enumerate(nums):
            diff = target - n
            if diff in indices and indices[diff] != i:
                return [i, indices[diff]]
	return []

	# Hash Map (One Pass) [T-O(n), S-O(n)]
	prevMap = {}  # val -> index

        for i, n in enumerate(nums):
            diff = target - n
            if diff in prevMap:
                return [prevMap[diff], i]
            prevMap[n] = i
	return [] 
```
> 49. Group Anagrams   

```
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        res = defaultdict(list)

	# Sorting [T-O(m * nlogn), S-(m*n)]
	# Where mm is the number of strings and nn is the length of the longest string.
        for s in strs:
            sortedS = ''.join(sorted(s))
            res[sortedS].append(s)
        return list(res.values()) 

	# Hash Table [T-O(m*n), S-(m*n)]
	for s in strs:
            count = [0] * 26
            for c in s:
                count[ord(c) - ord('a')] += 1
            res[tuple(count)].append(s)
        return list(res.values()) 
```
> 347. Top K Frequent Elements   

```
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = {}
        for num in nums:
            count[num] = 1 + count.get(num, 0)

	# Sorting [T-nlogn, S-O(n)]
        arr = []
        for num, cnt in count.items():
            arr.append([cnt, num])
        arr.sort()

        res = []
        while len(res) < k:
            res.append(arr.pop()[1])
        return res

	# Min-Heap [T-O(nlogk), S-O(n+k)]
	heap = []
        for num in count.keys():
            heapq.heappush(heap, (count[num], num))
            if len(heap) > k:
                heapq.heappop(heap)

        res = []
        for i in range(k):
            res.append(heapq.heappop(heap)[1])
        return res

	# Bucket Sort [T-O(n), S-O(n)]
        freq = [[] for i in range(len(nums) + 1)]
        for num, cnt in count.items():
            freq[cnt].append(num)

        res = []
        for i in range(len(freq) - 1, 0, -1):
            for num in freq[i]:
                res.append(num)
                if len(res) == k:
                    return res 
```
> 36. Valid Sudoku   

```
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:

	# Brute Force [T-O(n^2), S-O(n^2)]
	for row in range(9):
            seen = set()
            for i in range(9):
                if board[row][i] == ".": 
                    continue
                if board[row][i] in seen:
                    return False
                seen.add(board[row][i])

        for col in range(9):
            seen = set()
            for i in range(9):
                if board[i][col] == ".":
                    continue
                if board[i][col] in seen:
                    return False
                seen.add(board[i][col])

        for square in range(9):
            seen = set()
            for i in range(3):
                for j in range(3):
                    row = (square//3) * 3 + i
                    col = (square % 3) * 3 + j
                    if board[row][col] == ".":
                        continue
                    if board[row][col] in seen:
                        return False
                    seen.add(board[row][col])
        return True

	# Hash Set (One Pass) [T-O(n^2), S-O(n^2)]
	cols = defaultdict(set)
        rows = defaultdict(set)
        squares = defaultdict(set)  

        for r in range(9):
            for c in range(9):
                if board[r][c] == ".":
                    continue
                if ( board[r][c] in rows[r]
                    or board[r][c] in cols[c]
                    or board[r][c] in squares[(r // 3, c // 3)]):
                    return False

                cols[c].add(board[r][c])
                rows[r].add(board[r][c])
                squares[(r // 3, c // 3)].add(board[r][c])

        return True

	# Bitmask [T-O(n^2), S-O(n)]
	rows = [0] * 9
        cols = [0] * 9
        squares = [0] * 9

        for r in range(9):
            for c in range(9):
                if board[r][c] == ".":
                    continue

                val = int(board[r][c]) - 1
                if (1 << val) & rows[r]:
                    return False
                if (1 << val) & cols[c]:
                    return False
                if (1 << val) & squares[(r // 3) * 3 + (c // 3)]:
                    return False

                rows[r] |= (1 << val)
                cols[c] |= (1 << val)
                squares[(r // 3) * 3 + (c // 3)] |= (1 << val)

        return True 
```
> 128. Longest Consecutive Sequence   

```
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
	if not nums:
            return 0
        res = 0

	# brute force [T-O(n^2), S-O(n)]
        store = set(nums)

        for num in nums:
            streak, curr = 0, num
            while curr in store:
                streak += 1
                curr += 1
            res = max(res, streak)
        return res

	# Sorting [T-O(nlogn), S-O(1)]
        nums.sort()

        curr, streak = nums[0], 0
        i = 0
        while i < len(nums):
            if curr != nums[i]:
                curr = nums[i]
                streak = 0
            while i < len(nums) and nums[i] == curr:
                i += 1
            streak += 1
            curr += 1
            res = max(res, streak)
        return res

	# Hash Set [T-O(n), S-O(n)]
	numSet = set(nums)

        for num in numSet:
            if (num - 1) not in numSet:
                length = 1
                while (num + length) in numSet:
                    length += 1
                res = max(length, res)
        return res

	# Hash map [T-O(n), S-O(n)]
	mp = defaultdict(int)

	for num in nums:
            if not mp[num]:
                mp[num] = mp[num - 1] + mp[num + 1] + 1
                mp[num - mp[num - 1]] = mp[num]
                mp[num + mp[num + 1]] = mp[num]
                res = max(res, mp[num])
        return res

Example Walkthrough:

Let nums = [100, 4, 200, 1, 3, 2]

    res = 0, mp = {}

    num = 100:

        mp[100] is 0.

        mp[100] = mp[99] + mp[101] + 1 = 0 + 0 + 1 = 1.

        mp[100 - 0] (i.e., mp[100]) = 1.

        mp[100 + 0] (i.e., mp[100]) = 1.

        res = max(0, 1) = 1.

        mp = {100: 1}

    num = 4:

        mp[4] is 0.

        mp[4] = mp[3] + mp[5] + 1 = 0 + 0 + 1 = 1.

        mp[4 - 0] (i.e., mp[4]) = 1.

        mp[4 + 0] (i.e., mp[4]) = 1.

        res = max(1, 1) = 1.

        mp = {100: 1, 4: 1}

    num = 200: (Similar to 100, mp[200] = 1, res = 1)

        mp = {100: 1, 4: 1, 200: 1}

    num = 1:

        mp[1] is 0.

        mp[1] = mp[0] + mp[2] + 1 = 0 + 0 + 1 = 1.

        mp[1 - 0] (i.e., mp[1]) = 1.

        mp[1 + 0] (i.e., mp[1]) = 1.

        res = max(1, 1) = 1.

        mp = {100: 1, 4: 1, 200: 1, 1: 1}

    num = 3:

        mp[3] is 0.

        mp[3] = mp[2] + mp[4] + 1

            mp[2] is 0 (from defaultdict)

            mp[4] is 1 (from previous processing)

            So, mp[3] = 0 + 1 + 1 = 2.

        mp[3 - mp[2]] (i.e., mp[3 - 0], which is mp[3]) = 2.

        mp[3 + mp[4]] (i.e., mp[3 + 1], which is mp[4]) = 2.  (Now mp[4] is updated to reflect the sequence 3,4)

        res = max(1, 2) = 2.

        mp = {100: 1, 4: 2, 200: 1, 1: 1, 3: 2}

    num = 2:

        mp[2] is 0.

        mp[2] = mp[1] + mp[3] + 1

            mp[1] is 1.

            mp[3] is 2.

            So, mp[2] = 1 + 2 + 1 = 4.

        mp[2 - mp[1]] (i.e., mp[2 - 1], which is mp[1]) = 4. (Now mp[1] is updated to reflect the sequence 1,2,3,4)

        mp[2 + mp[3]] (i.e., mp[2 + 2], which is mp[4]) = 4. (Now mp[4] is updated to reflect the sequence 1,2,3,4)

        res = max(2, 4) = 4.

        mp = {100: 1, 4: 4, 200: 1, 1: 4, 3: 2, 2: 4}

Finally, the function returns res = 4. 
```

---
title: Recursion
draft: false
tags: 
date: 19-Aug-2025
---
# Problems
### Factorial
```python
# Recursive implementation of n! (n-factorial) calculation
def factorial(n):
    # Base case: n = 0 or 1
    if n <= 1:
        return 1

    # Recursive case: n! = n * (n - 1)!
    return n * factorial(n - 1)
```
### Fibonacci Sequence 
```python
# Recursive implementation to calculate the n-th Fibonacci number
def fibonacci(n):
    # Base case: n = 0 or 1
    if n <= 1:
        return n

    # Recursive case: fib(n) = fib(n - 1) + fib(n - 1)
    return fibonacci(n - 1) + fibonacci(n - 2)
```
- https://leetcode.com/problems/string-to-integer-atoi/
    
    ```cpp
    // O(n) O(1)
    int myAtoi(string s) {
        int i=0;
        int sign=1;
        long long ans=0;
    
        while(i < s.length() && s[i] == ' ')
            i++;
    
        if(s[i] == '-') sign=-1, i++;
        else if(s[i] == '+') i++;
    
        while(i < s.length()) {
            if(s[i]>='0' && s[i]<='9') {
                ans=ans*10+(s[i]-'0');
                
                if(ans>INT_MAX && sign==-1)
                    return INT_MIN;
                else if(ans>INT_MAX && sign==1)
                    return INT_MAX;
                i++;
            }
            else
                return ans*sign;
        }
        return (ans*sign);
    }
    ```
    
- https://leetcode.com/problems/powx-n/
    
    ```cpp
    // recursive solution
    // brute force O(n) O(n)
    int recursivePower(int x,int n) {
      if(n == 0) return 1;
      return x*recursivePower(x,n-1);
    }
    
    // binary exponentiation O(logn) O(logn)
    int binaryExponentiation(int x,int n) {
        if(n==0) return 1;
        else if(n%2 == 0)        
            return binaryExponentiation(x*x,n/2);
        else                             
            return x*binaryExponentiation(x*x,(n-1)/2);
    }
    
    // modulo exponentiation O(logn) O(logn)
    int modularExponentiation(int x, int n, int MOD) {
        if(n==0) return 1;
        else if(n%2 == 0)        
            return modularExponentiation((x*x) % MOD n/2, MOD);
        else                             
            return (x*modularExponentiation((x*x) % MOD, (n-1)/2, MOD)) % MOD;
    }
    
    // iterative solution
    double myPow(double x, int n) {
        double ans = 1.0;
        
        // brute force O(n) O(1) 
        for (int i = 0; i < n; i++) {
          ans = ans * x;
        }
        
        // binary exponentiation O(logn) O(1)
        long long nn = n;
    	  if (nn < 0) nn = -1 * nn;
    	  while (nn) {
    	    if (nn % 2) {
    	      ans = ans * x;
    	      nn--;
    	    } else {
    	      x = x * x;
    	      nn = nn / 2;
    	    }
    	  }
    	  if (n < 0) ans = (double)(1.0) / (double)(ans);
    	  return ans;
    }
    ```
    
- https://leetcode.com/problems/count-good-numbers/
    
    ```cpp
    // O(logn) O(1)
    int MOD = 1e9 + 7;
    
    long long power (long long x, long long n) {
        if (x == 0) return 0;
    
        long long ans = 1;
        x = x % MOD;
        
        while (n > 0) {
            if (n & 1) ans = (ans * x) % MOD;
            x = (x * x) % MOD;
            n = n >> 1;            
        }
        return ans;
    }
    
    int countGoodNumbers(long long n) {
        long long count4s = n/2;
        long long count5s = n - count4s;
        long long ans = ((power(4LL, count4s) % MOD * power(5LL, count5s) % MOD) % MOD);
        return (int)ans;
    }
    ```
    
- [Sort a Stack using Recursion](https://www.geeksforgeeks.org/dsa/sort-a-stack-using-recursion/)
    
    ```cpp
    // O(n^2) O(1) due to call stack and temporary stack.
    void sortedInsert(stack<int> &s, int x) {
        if (s.empty() || x > s.top()) {
            s.push(x);
            return;
        }
        int temp = s.top();
        s.pop();
        sortedInsert(s, x);
        s.push(temp);
    }
    
    void sortStack(stack<int> &s) {
        if (!s.empty()) {
            int x = s.top();
            s.pop();
            sortStack(s);
            sortedInsert(s, x);
        }
    }
    ```
    
- [How to Reverse a Stack using Recursion](https://www.geeksforgeeks.org/dsa/reverse-a-stack-using-recursion/)
    
    ```cpp
    // O(n^2) O(1) due to call stack and temporary stack.
    void insertAtBottom(stack<int>& s, int x) {
        if (s.size() == 0) {
            s.push(x);
        } else {
            int a = s.top();
            s.pop();
            insertAtBottom(s, x);
            s.push(a);
        }
    }
    
    void reverseStack(stack<int>& s) {
        if (s.size() > 0) {
            int x = s.top();
            s.pop();
            reverseStack(s);
            insertAtBottom(s, x);
        }
    }
    ```
    

# Subsequences

- [Generate all binary strings](https://www.geeksforgeeks.org/problems/generate-all-binary-strings/1)
    
    ```cpp
    // O(2^n) O(n)
    void printTheArray(int arr[], int n) {
        for (int i = 0; i < n; i++) {
            cout << arr[i] << " ";
        }
        cout << endl;
    }
    
    void generateAllBinaryStrings(int n, int arr[], int i) {
        if (i == n) {
            printTheArray(arr, n);
            return;
        }
        arr[i] = 0;
        generateAllBinaryStrings(n, arr, i + 1);
        arr[i] = 1;
        generateAllBinaryStrings(n, arr, i + 1);
    }
    
    int main() {
        int n = 4;
        int arr[n];
        generateAllBinaryStrings(n, arr, 0);
        return 0;
    }
    ```
    
- https://leetcode.com/problems/generate-parentheses/
    
    ```cpp
    // brute force O(2^n * n) O(n)
    generate all possible combinations of parentheses and check if it is balance or not. If a sequence is balanced, we store it as a valid result.
    
    // backtracking O(Cn × n) O(n)
    void validParenthesis(int n, int open, string cur, vector<string>& ans) {
        if (cur.length() == 2*n) {
            ans.push_back(cur);
            return;
        }
    
    		// Add opening parenthesis if we haven't used all n opening parentheses
        if (open < n) 
            validParenthesis(n, open+1, cur+"(", ans);
        // Add closing parenthesis if the number of closing
        // parentheses is less than the number of opening ones
        if (cur.length() - open < open) 
            validParenthesis(n, open, cur+")", ans);
    }
    
    vector<string> generateParenthesis(int n) {
        vector<string> ans;
        validParenthesis(n, 0, "", ans);
        return ans;
    }
    ```
    
- https://leetcode.com/problems/subsets/
    
    ```cpp
    // bit manipulation O(2^n * n) O(2^n * n)
    vector<string> AllPossibleStrings(string s) {
    	int n = s.length();
    	vector<string>ans;
    	for (int num = 0; num < (1 << n); num++) {
    		string sub = "";
    		for (int i = 0; i < n; i++) {
    			//check if the ith bit is set or not
    			if (num & (1 << i)) {
    				sub += s[i];
    			}
    		}
    		if (sub.length() > 0) {
    			ans.push_back(sub);
    		}
    	}
    	sort(ans.begin(), ans.end());
    	return ans;
    }
    
    // back tracking O(2^n) O(n) (recursion stack)
    // for string subsequence
    void solve(int i, string s, string &f) {
    	if (i == s.length()) {
    		cout << f << " ";
    		return;
    	}
    	//picking 
    	f = f + s[i];
    	solve(i + 1, s,  f);
    	//poping out while backtracking
    	f.pop_back();
    	solve(i + 1, s,  f);
    }
    
    string s = "abc";
    string f = "";
    cout << "All possible subsequences are: " << endl;
    solve(0, s, f);
    
    // for array (leetcode)
    void generateSubset(int i, vector<vector<int>> &ans, vector<int> &subset, vector<int>& nums, int n) {
        if (i >= n) {
            ans.push_back(subset);
            return;
        }      
        subset.push_back(nums[i]);
        generateSubset(i+1, ans, subset, nums, n);
        subset.pop_back();
        generateSubset(i+1, ans, subset, nums, n);
    }
    
    vector<vector<int>> subsets(vector<int>& nums) {
       vector<vector<int>> ans;
       vector<int> subset;
       generateSubset(0, ans, subset, nums, nums.size());
       return ans;
    }
    ```
    
- [Find all subsequences with sum equals to K](https://www.geeksforgeeks.org/dsa/find-all-subsequences-with-sum-equals-to-k/)
    
    ```cpp
    // O(2 ^ n) O(n)
    void findSubsequence(int ind, int sum, int k, vector<int> &cur, vector<int> &arr, vector<vector<int>> &res) {
        int n = arr.size();
        
        if(ind == n) {
            if(sum == k) 
                res.push_back(cur);
            return;
        }
    
    		cur.push_back(arr[ind]);
        findSubsequence(ind + 1, sum + arr[ind], k, cur, arr, res);
        cur.pop_back();
        findSubsequence(ind + 1, sum, k, cur, arr, res);    
    }
    
    vector<vector<int>> subsequencesSumK(vector<int> &arr, int k) {
        vector<vector<int>> res;
        vector<int> cur;
        findSubsequence(0, 0, k, cur, arr, res);
        return res;
    }
    
    ```
    
- [Check if there exists a subsequence with sum K](https://www.geeksforgeeks.org/problems/check-if-there-exists-a-subsequence-with-sum-k/1)
    
    ```cpp
    // O(2^n) O(n)
    bool findSubsequence(int ind, vector<int> &arr, int sum, int k) {
        int n = arr.size();
        
        if(sum == k) return true;
        if (sum > k) return false;
        if(ind == n) return false;
        
        if (findSubsequence(ind + 1, arr, sum + arr[ind], k))
            return true;
        if (findSubsequence(ind + 1, arr, sum, k))
            return true;
        
        return false;
    }
    
    bool checkSubsequenceSum(int n, vector<int>& arr, int k) {
        return findSubsequence(0, arr, 0, k);
    }
    ```
    
- https://leetcode.com/problems/combination-sum/
    
    ![image.png](image%2033.png)
    
    ![image.png](image%2034.png)
    
    ![image.png](image%2035.png)
    
    ```cpp
    // O(2^t * k) O(k*x)
    // t = target, k = avg length of arr, x = no of combination
    void findCombination(int ind, int target, vector<int>& arr, vector<vector<int>>& ans, vector<int>& ds) {
      if (ind == arr.size()) {
        if (target == 0) {
          ans.push_back(ds);
        }
        return;
      }
      // pick up the element 
      if (arr[ind] <= target) {
        ds.push_back(arr[ind]);
        findCombination(ind, target - arr[ind], arr, ans, ds);
        ds.pop_back();
      }
      findCombination(ind + 1, target, arr, ans, ds);
    }
    
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
      vector<vector<int>> ans;
      vector<int> ds;
      findCombination(0, target, candidates, ans, ds);
      return ans;
    }
    ```
    
- https://leetcode.com/problems/combination-sum-ii/
    
    ![image.png](image%2036.png)
    
    ```cpp
    // O(2^n*k) O(k*x) 
    void findCombination(int ind, int target, vector<int>& arr, vector<vector<int>>& ans, vector<int>& ds) {
      if (target == 0) {
        ans.push_back(ds);
        return;
      }
      
      for (int i = ind; i < arr.size(); i++) {
        if (i > ind && arr[i] == arr[i - 1]) continue;
        if (arr[i] > target) break;
        ds.push_back(arr[i]);
        findCombination(i + 1, target - arr[i], arr, ans, ds);
        ds.pop_back();
      }
    }
    
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
      sort(candidates.begin(), candidates.end());
      vector<vector<int>> ans;
      vector<int> ds;
      findCombination(0, target, candidates, ans, ds);
      return ans;
    }
    ```
    
- [Subset Sum-I](https://takeuforward.org/data-structure/subset-sum-sum-of-all-subsets/)
    
    ```cpp
    // O(2^n)+O(2^n log(2^n)) O(2^n)
    void subsetSumsHelper(int ind, vector<int>& arr, int n, vector<int>& ans, int sum) {
      if (ind == n) {
        ans.push_back(sum);
        return;
      }
      //element is picked
      subsetSumsHelper(ind + 1, arr, n, ans, sum + arr[ind]);
      //element is not picked
      subsetSumsHelper(ind + 1, arr, n, ans, sum);
    }
      
    vector<int> subsetSums(vector<int> arr, int n) {
      vector<int> ans;
      subsetSumsHelper(0, arr, n, ans, 0);
      sort(ans.begin(), ans.end());
      return ans;
    }
    ```
    
- https://leetcode.com/problems/subsets-ii/
    
    ```cpp
    O(2^n*k) O(k*x)
    void findSubsets(int ind, vector<int>& nums, vector<int>& ds, vector<vector<int>>& ans) {
        ans.push_back(ds);
        for (int i = ind; i < nums.size(); i++) {
            if (i != ind && nums[i] == nums[i - 1])
                continue;
            ds.push_back(nums[i]);
            findSubsets(i + 1, nums, ds, ans);
            ds.pop_back();
        }
    }
    
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
    		sort(nums.begin(), nums.end());
        vector<vector<int>> ans;
        vector<int> ds;    
        findSubsets(0, nums, ds, ans);
        return ans;
    }
    ```
    
- https://leetcode.com/problems/combination-sum-iii/
    
    ```cpp
    // O(C(9,k) × k) O(k)
    void findCombination(int ind, int n, int target, vector<int>& ds, vector<vector<int>>& ans, int k) {
        if (target == 0 && ds.size() == k) {
            ans.push_back(ds);
            return;
        }
    
        for (int i = ind; i <=9; i++) {
            if (i > target) break;
            ds.push_back(i);
            findCombination(i + 1, n, target-i, ds, ans, k);
            ds.pop_back();
        }
    }
    
    vector<vector<int>> combinationSum3(int k, int n) {
        vector<vector<int>> ans;
        vector<int> ds;    
        int target = n;
        findCombination(1, n, target, ds, ans, k);
        return ans;
    }
    ```
    
- https://leetcode.com/problems/letter-combinations-of-a-phone-number/
    
    ```cpp
    // backtracking O(n∗4n) O(n) extra space. O(n∗4n) space for the output list.
    vector<string> res;
    vector<string> digitToChar = {"", "", "abc", "def", "ghi", "jkl", 
                                  "mno", "qprs", "tuv", "wxyz"};
    
    void backtrack(int i, string curStr, string &digits) {
        if (curStr.size() == digits.size()) {
            res.push_back(curStr);
            return;
        }
        
        string chars = digitToChar[digits[i] - '0'];
        for (char c : chars) {
            backtrack(i + 1, curStr + c, digits);
        }
    }
    
    vector<string> letterCombinations(string digits) {
        if (digits.empty()) return res;
        backtrack(0, "", digits);
        return res;
    }
    
    // iteration O(n∗4n) O(n) extra space. O(n∗4n) space for the output list.
    vector<string> letterCombinations(string digits) {
        if (digits.empty()) return {};
        
        vector<string> res = {""};
        vector<string> digitToChar = {
            "", "", "abc", "def", "ghi", "jkl",
            "mno", "qprs", "tuv", "wxyz"
        };
    
        for (char digit : digits) {
            vector<string> tmp;
            for (string &curStr : res) {
                for (char c : digitToChar[digit - '0']) {
                    tmp.push_back(curStr + c);
                }
            }
            res = tmp;
        }
        return res;
    }
    ```
    

# Backtracking
### Determine if a path exists from the root of the tree to a leaf tree. It may not contain any zeros 
```python
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None

def canReachLeaf(root):
    if not root or root.val == 0:
        return False
    
    if not root.left and not root.right:
        return True
    if canReachLeaf(root.left):
        return True
    if canReachLeaf(root.right):
        return True
    return False

def leafPath(root, path):
    if not root or root.val == 0:
        return False
    path.append(root.val)

    if not root.left and not root.right:
        return True
    if leafPath(root.left, path):
        return True
    if leafPath(root.right, path):
        return True
    path.pop()
    return False
```
## subsets
### subset implementation
```python
# Time: O(n * 2^n), Space: O(n)
def subsetsWithoutDuplicates(nums):
    subsets, curSet = [], []
    helper(0, nums, curSet, subsets)
    return subsets

def helper(i, nums, curSet, subsets):
    if i >= len(nums):
        subsets.append(curSet.copy())
        return
    
    # decision to include nums[i]
    curSet.append(nums[i])
    helper(i + 1, nums, curSet, subsets)
    curSet.pop()

    # decision NOT to include nums[i]
    helper(i + 1, nums, curSet, subsets)


# Time: O(n * 2^n), Space: O(n)
def subsetsWithDuplicates(nums):
    nums.sort()
    subsets, curSet = [], []
    helper2(0, nums, curSet, subsets)
    return subsets

def helper2(i, nums, curSet, subsets):
    if i >= len(nums):
        subsets.append(curSet.copy())
        return
    
    # decision to include nums[i]
    curSet.append(nums[i])
    helper2(i + 1, nums, curSet, subsets)
    curSet.pop()

    # decision NOT to include nums[i]
    while i + 1 < len(nums) and nums[i] == nums[i + 1]:
        i += 1
    helper2(i + 1, nums, curSet, subsets)
```
## Combinations
### combination implementation
```python
# Given n numbers (1 - n), return all possible combinations
# of size k. (n choose k math problem).
# Time: O(k * 2^n)
def combinations(n, k):
    combs = []
    helper(1, [], combs, n, k)
    return combs

def helper(i, curComb, combs, n, k):
    if len(curComb) == k:
        combs.append(curComb.copy())
        return
    if i > n:
        return
    
    # decision to include i
    curComb.append(i)
    helper(i + 1, curComb, combs, n, k)
    curComb.pop()
    
    # decision to NOT include i
    helper(i + 1, curComb, combs, n, k)


# Time: O(k * C(n, k))
def combinations2(n, k):
    combs = []
    helper2(1, [], combs, n, k)
    return combs

def helper2(i, curComb, combs, n, k):
    if len(curComb) == k:
        combs.append(curComb.copy())
        return
    if i > n:
        return
    
    for j in range(i, n + 1):
        curComb.append(j)
        helper2(j + 1, curComb, combs, n, k)
        curComb.pop()
```
## Permutation
```python
# Time: O(n^2 * n!)
def permutationsRecursive(nums):
    return helper(0, nums)
        
def helper(i, nums):   
    if i == len(nums):
        return [[]]
    
    resPerms = []
    perms = helper(i + 1, nums)
    for p in perms:
        for j in range(len(p) + 1):
            pCopy = p.copy()
            pCopy.insert(j, nums[i])
            resPerms.append(pCopy)
    return resPerms


# Time: O(n^2 * n!)
def permutationsIterative(nums):
    perms = [[]]

    for n in nums:
        nextPerms = []
        for p in perms:
            for i in range(len(p) + 1):
                pCopy = p.copy()
                pCopy.insert(i, n)
                nextPerms.append(pCopy)
        perms = nextPerms
    return perms1
```

- https://leetcode.com/problems/palindrome-partitioning/
    
    ```cpp
    // O((2^n)*k*(n/2)) O(k * x)
    // O(k) k=avg length of palindrome
    // O(2^n) to generate every substring
    // O(n/2)  to check if the substring generated is a palindrome.
    void partitionHelper(int index, string s, vector<string>& path, vector<vector<string>>& res) {
      if (index == s.size()) {
        res.push_back(path);
        return;
      }
      
      for (int i = index; i < s.size(); ++i) {
        if (isPalindrome(s, index, i)) { 
          path.push_back(s.substr(index, i - index + 1));
          partitionHelper(i + 1, s, path, res); 
          path.pop_back();
        }
      }
    }
    
    bool isPalindrome(string s, int start, int end) {
      while (start <= end) {
        if (s[start++] != s[end--])
          return false;
      }
      return true;
    }
    
    vector<vector<string>> partition(string s) {
      vector<vector<string>> res;
      vector<string> path;
      partitionHelper(0, s, path, res);
      return res;
    }
    ```
    
- https://leetcode.com/problems/word-search/
    
    ```cpp
    // O(m*n*4^k) O(k)
    // k is the length of the word.
    // 4^k is because at each level of our decision tree we are making 4 recursive calls
    bool searchNext(vector<vector<char>> &board, string word, int row, int col, 
        int index, int m, int n) {
        if (index == word.length())
            return true;
    
        if (row < 0 || col < 0 || row == m || col == n || board[row][col] != 
        word[index] or board[row][col] == '!')
            return false;
    
        char c = board[row][col];
        board[row][col] = '!';
    
        // top direction
        bool top = searchNext(board, word, row - 1, col, index + 1, m, n);
        // right direction
        bool right = searchNext(board, word, row, col + 1, index + 1, m, n);
        // bottom direction
        bool bottom = searchNext(board, word, row + 1, col, index + 1, m, n);
        // left direction
        bool left = searchNext(board, word, row, col - 1, index + 1, m, n);
    
        board[row][col] = c; // undo change
    
        return top || right || bottom || left;
    }
    
    bool exist(vector<vector<char>> board, string word) {
        int m = board.size();
        int n = board[0].size();
        int index = 0;
    
        // First search the first character
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == word[index]) {
                    if (searchNext(board, word, i, j, index, m, n))
                        return true;
                }
            }
        }
        return false;
    }
    
    ```
    
- https://leetcode.com/problems/n-queens/
    
    ![image.png](image%2037.png)
    
    ![image.png](image%2038.png)
    
    ![image.png](image%2039.png)
    
    ![image.png](image%2040.png)
    
    ![image.png](image%2041.png)
    
    ![image.png](image%2042.png)
    
    ![image.png](image%2043.png)
    
    ![image.png](image%2044.png)
    
    ![image.png](image%2045.png)
    
    ```cpp
    // (N! * N) nearly. O(n^2) (if isSafe) O(n) (if optimized)
    class Solution {
      public:
        bool isSafe1(int row, int col, vector < string > board, int n) {
          // check upper element
          int duprow = row;
          int dupcol = col;
    
          while (row >= 0 && col >= 0) {
            if (board[row][col] == 'Q')
              return false;
            row--;
            col--;
          }
    
          col = dupcol;
          row = duprow;
          while (col >= 0) {
            if (board[row][col] == 'Q')
              return false;
            col--;
          }
    
          row = duprow;
          col = dupcol;
          while (row < n && col >= 0) {
            if (board[row][col] == 'Q')
              return false;
            row++;
            col--;
          }
          return true;
        }
    
      public:
        void solve(int col, vector < string > & board, vector < vector < string >> & ans, int n) {
          if (col == n) {
            ans.push_back(board);
            return;
          }
          
          // O(n^2) space complexity
          for (int row = 0; row < n; row++) {
            if (isSafe1(row, col, board, n)) {
              board[row][col] = 'Q';
              solve(col + 1, board, ans, n);
              board[row][col] = '.';
            }
          }
          
          // O(n) space complexity
    	    for (int row = 0; row < n; row++) {
            if (leftrow[row] == 0 && lowerDiagonal[row + col] == 0 && upperDiagonal[n - 1 + col - row] == 0) {
              board[row][col] = 'Q';
              leftrow[row] = 1;
              lowerDiagonal[row + col] = 1;
              upperDiagonal[n - 1 + col - row] = 1;
              solve(col + 1, board, ans, leftrow, upperDiagonal, lowerDiagonal, n);
              board[row][col] = '.';
              leftrow[row] = 0;
              lowerDiagonal[row + col] = 0;
              upperDiagonal[n - 1 + col - row] = 0;
            }
          }
        }
    
      public:
        vector<vector<string>> solveNQueens(int n) {
          vector<vector<string>> ans;
          vector<string> board(n);
          string s(n, '.');
          for (int i = 0; i < n; i++) {
            board[i] = s;
          }
          solve(0, board, ans, n);
          return ans;
        }
    };
    ```
    
- [Rat in a Maze](https://takeuforward.org/data-structure/rat-in-a-maze/)
    
    ```cpp
    // O(4^(m*n)) O(m*n)
    class Solution {
      void findPathHelper(int i, int j, vector<vector<int>>& a, int n, vector<string>& ans, string move, vector<vector<int>>& vis) {
        if (i == n - 1 && j == n - 1) {
          ans.push_back(move);
          return;
        }
    
        // downward
        if (i + 1 < n && !vis[i + 1][j] && a[i + 1][j] == 1) {
          vis[i][j] = 1;
          findPathHelper(i + 1, j, a, n, ans, move + 'D', vis);
          vis[i][j] = 0;
        }
    
        // left
        if (j - 1 >= 0 && !vis[i][j - 1] && a[i][j - 1] == 1) {
          vis[i][j] = 1;
          findPathHelper(i, j - 1, a, n, ans, move + 'L', vis);
          vis[i][j] = 0;
        }
    
        // right 
        if (j + 1 < n && !vis[i][j + 1] && a[i][j + 1] == 1) {
          vis[i][j] = 1;
          findPathHelper(i, j + 1, a, n, ans, move + 'R', vis);
          vis[i][j] = 0;
        }
    
        // upward
        if (i - 1 >= 0 && !vis[i - 1][j] && a[i - 1][j] == 1) {
          vis[i][j] = 1;
          findPathHelper(i - 1, j, a, n, ans, move + 'U', vis);
          vis[i][j] = 0;
        }
    
      }
      
      public:
        vector<string> findPath(vector<vector<int>>& m, int n) {
          vector<string> ans;
          vector<vector<int>> vis(n, vector<int> (n, 0));
    
          if (m[0][0] == 1) findPathHelper(0, 0, m, n, ans, "", vis);
          return ans;
        }
    };
    ```
    
- https://leetcode.com/problems/word-break/
    
    ```cpp
    // backtracking O(2^N) O(N)
    bool wordBreak(string s, unordered_set<string> &set, int start){
        if(start == s.size()){
            return true;
        }
        for(int i=start; i<s.size(); i++){
            if(set.count(s.substr(start, i+1-start)) && wordBreak(s, set, i+1)){
                return true;
            }
        }
        return false;
    }
    
    bool wordBreak(string s, vector<string>& wordDict) {
        unordered_set<string> set(wordDict.begin(), wordDict.end());
        return wordBreak(s, set, 0);
    }
    
    // memoization O(N^3) O(N)
    bool wordBreak(string s, unordered_set<string> &set, vector<int> &memo, int start){
        if(start == s.size()){
            return true;
        }
        if(memo[start] != -1){
            return memo[start];
        }
        for(int i=start; i<s.size(); i++){
            if(set.count(s.substr(start, i+1-start)) && wordBreak(s, set, memo, i+1)){
                memo[start] = true;
                return true;
            }
        }
        return memo[start] = false;
    }
    
    bool wordBreak(string s, vector<string>& wordDict) {
        vector<int> memo(s.size(), -1);
        unordered_set<string> set(wordDict.begin(), wordDict.end());
        return wordBreak(s, set, memo, 0);
    }
    
    // dp tabulation O(N^3) O(N)
    bool wordBreak(string s, vector<string>& wordDict) {
        vector<bool> dp(s.size()+1, 0);
        dp[0] = true;
        unordered_set<string> set(wordDict.begin(), wordDict.end());
        for(int i=1; i<=s.size(); i++){
            for(int j=0; j<i; j++){
                if(dp[j] && set.count(s.substr(j, i-j))){
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[s.size()];
    }
    ```
    
- [M Coloring Problem](https://takeuforward.org/data-structure/m-coloring-problem/)
    
    ```cpp
    bool isSafe(int node, int color[], bool graph[101][101], int n, int col) {
      for (int k = 0; k < n; k++) {
        if (k != node && graph[k][node] == 1 && color[k] == col) {
          return false;
        }
      }
      return true;
    }
    
    bool solve(int node, int color[], int m, int N, bool graph[101][101]) {
      if (node == N) return true;
    
      for (int i = 1; i <= m; i++) {
        if (isSafe(node, color, graph, N, i)) {
          color[node] = i;
          if (solve(node + 1, color, m, N, graph)) return true;
          color[node] = 0;
        }
    
      }
      return false;
    }
    
    //Function to determine if graph can be coloured with at most M colours such
    //that no two adjacent vertices of graph are coloured with same colour.
    bool graphColoring(bool graph[101][101], int m, int N) {
      int color[N] = { 0 };
      if (solve(0, color, m, N, graph)) return true;
      return false;
    }
    ```
    
- https://leetcode.com/problems/sudoku-solver/
    
    ```cpp
    bool isValid(vector<vector<char>>& board, int row, int col, char c) {
      for (int i = 0; i < 9; i++) {
        if (board[i][col] == c)
          return false;
    
        if (board[row][i] == c)
          return false;
    
        if (board[3 * (row / 3) + i / 3][3 * (col / 3) + i % 3] == c)
          return false;
      }
      return true;
    }
    
    bool solveSudoku(vector<vector<char>> & board) {
      for (int i = 0; i < board.size(); i++) {
        for (int j = 0; j < board[0].size(); j++) {
          if (board[i][j] == '.') {
            for (char c = '1'; c <= '9'; c++) {
              if (isValid(board, i, j, c)) {
                board[i][j] = c;
                if (solveSudoku(board))
                  return true;
                else
                  board[i][j] = '.';
              }
            }
            return false;
          }
        }
      }
      return true;
    }
    ```
    
- https://leetcode.com/problems/expression-add-operators/
    
    ```cpp
    // O(3^n) O(n^3) Worst Case Scenario where n is num size. 
    void recursiveCall(int i, string sumPath, long sum, long prev, string num, int target, vector<string> &result) {
        if (i == num.size()) {
            if (sum == target)
                result.push_back(sumPath);
            return;
        }
    
        for (int j = i; j < num.size(); j++) {
            if (j > i && num[i] == '0') break;
    
            long number = stol(num.substr(i, j - i + 1));
            string tempPath = num.substr(i, j - i + 1);
    
            if (i == 0) 
                recursiveCall(j + 1, tempPath, number, number, num, target, result);
            else {
                recursiveCall(j + 1, sumPath + '+' + tempPath, sum + number, number, num, target, result);
                recursiveCall(j + 1, sumPath + '-' + tempPath, sum - number, -number, num, target, result);
                recursiveCall(j + 1, sumPath + '*' + tempPath, sum - prev + (prev *number), prev * number, num, target, result);
            }
        }
    }
    
    vector<string> addOperators(string num, int target) {
        vector<string> ans;
        recursiveCall(0, "", 0, 0, num, target, ans);
        return ans;
    }
    ```
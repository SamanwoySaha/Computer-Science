---
title: Stacks and Queues
draft: false
tags: 
date: 19-Aug-2025
---
# Stacks
## Data Structure
```python
class Stack:
    def __init__(self):
        self.stack = []

    def push(self, n):
        self.stack.append(n)

    def pop(self):
        return self.stack.pop()
```

- [Implement Stack using Arrays](https://takeuforward.org/data-structure/implement-stack-using-array/)
    
    ```cpp
    // O(n) O(n)
    class Stack {
      int size;
      int *arr;
      int top;
      
      public:
        Stack() {
          top = -1;
          size = 1000;
          arr = new int[size];
        }
        
    	  void push(int x) {
    	    top++;
    	    arr[top] = x;
    	  }
    	  
    	  int pop() {
    	    int x = arr[top];
    	    top--;
    	    return x;
    	  }
    	  
    	  int Top() {
    	    return arr[top];
    	  }
    	  
    	  int Size() {
    	    return top + 1;
    	  }
    };
    ```
    
- https://leetcode.com/problems/implement-stack-using-queues/
    
    ```cpp
    // O(n) O(n)
    class Stack {
      queue<int> q;
      public:
        void Push(int x) {
          int s = q.size();
          q.push(x);
          for (int i = 0; i < s; i++) {
            q.push(q.front());
            q.pop();
          }
        }
        
    	  int Pop() {
    	    int n = q.front();
    	    q.pop();
    	    return n;
    	  }
    	  
    	  int Top() {
    	    return q.front();
    	  }
    	  
    	  int Size() {
    	    return q.size();
    	  }
    	  
    	  bool empty() {
            return q.size() == 0;
        }
    };
    ```
    
- [Implement stack using Linkedlist](https://takeuforward.org/data-structure/implement-stack-using-linked-list/)
    
    ```cpp
    struct stackNode {
      int data;
      stackNode *next;
      int size;
      stackNode(int d) {
        data = d;
        next = NULL;
      }
    };
    
    struct stack {
      stackNode *top;
      int size;
      stack() {
        top = NULL;
        size = 0;
      }
      
      void stackPush(int x) {
        stackNode *element = new stackNode(x);
        element -> next = top;
        top = element;
        cout << "Element pushed" << "\n";
        size++;
      }
      
      int stackPop() {
        if (top == NULL) 
          return -1;
        
        int topData = top -> data;
        stackNode * temp = top;
        top = top -> next;
        delete temp;
        size--;
        return topData;
      }
      
      int stackSize() {
        return size;
      }
      
      bool stackIsEmpty() {
        return top == NULL;
      }
      
      int stackPeek() {
        if (top == NULL) return -1;
        return top -> data;
      }
      
      void printStack() {
        stackNode *current = top;
        while (current != NULL) {
          cout << current -> data << " ";
          current = current -> next;
        }
      }
    };
    ```
    
- https://leetcode.com/problems/valid-parentheses/
    
    ```cpp
    // O(n) O(n)
    bool isValid(string s) {
        stack<char> st; 
        for(auto it: s) {
            if(it == '(' || it == '{' || it == '[') 
    	        st.push(it); 
            else {
                if(st.size() == 0) return false; 
                char ch = st.top(); 
                st.pop(); 
                if((it == ')' and ch == '(') or  (it == ']' and ch == '[') or (it == '}' and ch == '{')) 
    	            continue;
                else 
    	            return false;
            }
        }
        return st.empty(); 
    }
    ```
    
- https://leetcode.com/problems/min-stack/
    
    ```cpp
    // O(1) O(2n)
    class MinStack {
      stack<pair<int, int>> st;
    
      public:
        void push(int x) {
          int min;
          if (st.empty()) {
            min = x;
          } else {
            min = min(st.top().second, x);
          }
          st.push({x,min});
        }
    
    	  void pop() {
    	    st.pop();
    	  }
    	
    	  int top() {
    	    return st.top().first;
    	  }
    	
    	  int getMin() {
    	    return st.top().second;
    	  }
    };
    
    // O(1) O(n)
    class MinStack {
      stack<long long> st;
      long long mini;
      public:
        MinStack() {
          while (st.empty() == false) st.pop();
          mini = INT_MAX;
        }
    
    	  void push(int value) {
    	    long long val = Long.valuevalue;
    	    if (st.empty()) {
    	      mini = val;
    	      st.push(val);
    	    } else {
    	      if (val < mini) {
    	        st.push(2 *val*1LL - mini);
    	        mini = val;
    	      } else {
    	        st.push(val);
    	      }
    	    }
    	  }
    	
    	  void pop() {
    	    if (st.empty()) return;
    	    long long el = st.top();
    	    st.pop();
    	
    	    if (el < mini) {
    	      mini = 2 * mini - el;
    	    }
    	  }
    	
    	  int top() {
    	    if (st.empty()) return -1;
    	
    	    long long el = st.top();
    	    if (el < mini) return mini;
    	    return el;
    	  }
    	
    	  int getMin() {
    	    return mini;
    	  }
    };
    ```
    

## Monotonic Stack

- https://leetcode.com/problems/next-greater-element-i/
    
    ```cpp
    // brute force O(n^2) O(n) two loops
    
    // optimal O(n) O(n)
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
        unordered_map<int, int> nge; 
        stack<int> st;
    
        for(int i=nums2.size()-1; i>=0; i--) {
    		    // maintain decreasing order
            while(!st.empty() && st.top() <= nums2[i]) 
                st.pop();
    
            if (st.empty()) nge[nums2[i]] = -1;
            else nge[nums2[i]] = st.top();
    
            st.push(nums2[i]);
        }
    
        vector<int> result;
        for (int num : nums1) {
            result.push_back(nge[num]);
        }
        
        return result;
    }
    ```
    
- https://leetcode.com/problems/next-greater-element-ii/
    
    ```cpp
    // O(n) O(n)
    vector<int> nextGreaterElements(vector<int>& nums) {
        int n = nums.size();
        vector<int> nge(n);
        stack<int> st;
    
        for (int i = 2*n-1; i >= 0; i--) {
    		    // maintain decreasing order
            while (!st.empty() && st.top() <= nums[i%n]) 
                st.pop();
            if (i < n) 
                nge[i] = st.empty() ? -1 : st.top();
            st.push(nums[i%n]);
        }
        return nge;
    }
    ```
    
- [Next Smaller Element](https://www.geeksforgeeks.org/dsa/next-smaller-element/)
    
    ```cpp
    // O(n) O(n)
    vector<int> findNextSmallerElement(const vector<int>& arr) {
        int n = arr.size();
        vector<int> nse(n, -1);
        stack<int> st;
    
        for (int i = 0; i < n; i++) {
    		    // maintain increasing order
            while (!st.empty() && arr[i] < arr[st.top()]) {
                nextSmaller[st.top()] = arr[i]; 
                st.pop(); 
            }
            st.push(i);
        }
        return nse;
    }
    ```
    
- [Number of NGEs to the right](https://www.geeksforgeeks.org/dsa/number-nges-right/)
    
    ```cpp
    // O(n) O(1)
    int nextGreaterElements(vector<int>& a, int index) {
        int count = 0, N = a.size();
        for (int i = index + 1; i < N; i++)
            if (a[i] > a[index])
                count++;
    
        return count;
    }
    ```
    

# Queues
## Data Structure
```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

class Queue:
    # Implementing this with dummy nodes would be easier!
    def __init__(self):
        self.left = self.right = None
    
    def enqueue(self, val):
        newNode = ListNode(val)

        # Queue is non-empty
        if self.right:
            self.right.next = newNode
            self.right = self.right.next
        # Queue is empty
        else:
            self.left = self.right = newNode

    def dequeue(self):
        # Queue is empty
        if not self.left:
            return None
        
        # Remove left node and return value
        val = self.left.val
        self.left = self.left.next
        return val

    def print(self):
        cur = self.left
        while cur:
            print(cur.val, ' -> ', end ="")
            cur = cur.next
        print() # new line
```

## Monotonic Queue
### [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)
```python
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
- [Implement Queue using Arrays](https://takeuforward.org/data-structure/implement-queue-using-array/)
    
    ```cpp
    // time: pop: O(1), push: O(1), top: O(1), size: O(1)
    // space: O(n)
    class Queue {
      int * arr;
      int start, end, currSize, maxSize;
      public:
        Queue() {
          arr = new int[16];
          start = -1;
          end = -1;
          currSize = 0;
        }
    
    	  Queue(int maxSize) {
    	    (*this).maxSize = maxSize;
    	    arr = new int[maxSize];
    	    start = -1;
    	    end = -1;
    	    currSize = 0;
    	  }
    	  
    	  void push(int newElement) {
    	    if (currSize == maxSize) {
    	      cout << "Queue is full\nExiting..." << endl;
    	      exit(1);
    	    }
    	    
    	    if (end == -1) {
    	      start = 0;
    	      end = 0;
    	    } else {
    	      end = (end + 1) % maxSize;
    	    }
    	    
    	    arr[end] = newElement;
    	    cout << "The element pushed is " << newElement << endl;
    	    currSize++;
    	  }
    	  
    	  int pop() {
    	    if (start == -1) {
    	      cout << "Queue Empty\nExiting..." << endl;
    	    }
    	    
    	    int popped = arr[start];
    	    if (currSize == 1) {
    	      start = -1;
    	      end = -1;
    	    } else {
    	      start = (start + 1) % maxSize;
    	    }
    	    
    	    currSize--;
    	    return popped;
    	  }
    	  
    	  int top() {
    	    if (start == -1) {
    	      cout << "Queue is Empty" << endl;
    	      exit(1);
    	    }
    	    return arr[start];
    	  }
    	  
    	  int size() {
    	    return currSize;
    	  }
    };
    
    ```
    
- https://leetcode.com/problems/implement-queue-using-stacks/
    
    ```cpp
    // Using two Stacks where push operation is O(N)
    // O(n) O(2n)
    struct Queue {
      stack<int> input, output;
      
      void Push(int data) {
        while (!input.empty()) {
          output.push(input.top());
          input.pop();
        }
    
        cout << "The element pushed is " << data << endl;
        input.push(data);
        while (!output.empty()) {
          input.push(output.top());
          output.pop();
        }
      }
    
      int Pop() {
        if (input.empty()) {
          cout << "Stack is empty";
          exit(0);
        }
        int val = input.top();
        input.pop();
        return val;
      }
    
      int Top() {
        if (input.empty()) {
          cout << "Stack is empty";
          exit(0);
        }
        return input.top();
      }
    
      int size() {
        return input.size();
      }
    };
    
    // Using two Stacks where push operation is O(1)
    // O(1) O(n)
    class MyQueue {
      public:
        stack<int> input, output;
    
      MyQueue() {
    
      }
    
      void push(int x) {
        cout << "The element pushed is " << x << endl;
        input.push(x);
      }
    
      int pop() {
        if (output.empty())
          while (input.size())
            output.push(input.top()), input.pop();
    
        int x = output.top();
        output.pop();
        return x;
      }
    
      int top() {
        if (output.empty())
          while (input.size())
            output.push(input.top()), input.pop();
        return output.top();
      }
    
      int size() {
        return (output.size() + input.size()); 
      }
    
    };
    ```
    
- [Implement queue using Linkedlist](https://takeuforward.org/data-structure/implement-queue-using-linked-list/)
    
    ```cpp
    // O(1) O(1)
    class QueueNode {
     public: 
        int val;
        QueueNode *next;
        QueueNode(int data) {
           val = data;
           next = nullptr;
        }
    };  
    
    QueueNode *Front = nullptr, *Rare = nullptr;
    
    class Queue {
    public:
        int size = 0;
        bool Empty();
        void Enqueue(int value);
        void Dequeue();
        int Peek();
    };  
    
    bool Queue ::  Empty() {
        return Front == nullptr;
    }  
    
    int Queue :: Peek() {
        if(Empty()) {
    	      cout<<"Queue is Empty"<<endl;
            return -1;
        } else 
          return Front->val;
    }  
     
    void Queue :: Enqueue(int value) {
        QueueNode *Temp;
        Temp = new QueueNode(value); 
        if (Temp == nullptr)  //When heap exhausted 
            cout << "Queue is Full" << endl;
        else {
            if (Front == nullptr) {
                Front = Temp;
                Rare = Temp;
            } 
            else {
                Rare->next = Temp;
                Rare = Temp;
            }
            cout << value << " Inserted into Queue " << endl;
            size++;
        } 
    }      
    
    void Queue :: Dequeue() {
        if (Front == nullptr) 
            cout << "Queue is Empty" << endl;
        else { 
            cout << Front->val << " Removed From Queue" << endl;
            QueueNode *Temp = Front;
            Front = Front->next;
            delete Temp;
            size--;
        }  
    }   
    ```
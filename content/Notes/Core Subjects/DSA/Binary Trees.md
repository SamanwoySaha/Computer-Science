---
title: Binary Trees
draft: false
tags: 
date: 19-Aug-2025
---
# Binary Trees

# Theory

- What is Binary Tree?
    
    ![image.png](image%2097.png)
    
    ![image.png](image%2098.png)
    
    - Every node can have maximum 2 children not more than that.
    - Left child and right child or down and right child
- number of binary trees using n nodes
    
    ![image.png](image%2099.png)
    
    ![image.png](image%20100.png)
    
    ![image.png](image%20101.png)
    
- Full Binary Tree
    
    every node has either zero or two children.
    
    ![image.png](image%20102.png)
    
    ![image.png](image%20103.png)
    
- Complete Binary Tree
    
    all levels are filled completely except possibly the last level, which is filled from left to right.
    
    ![image.png](image%20104.png)
    
    ![image.png](image%20105.png)
    
     it might seem similar to a full binary tree, a complete binary tree doesn't require all nodes to have two children; it's about the positioning and arrangement of nodes.
    
    ![image.png](image%20106.png)
    
- Perfect Binary Tree
    
    all leaf nodes are at the same level and the number of leaf nodes is maximised for that level.
    
    ![image.png](image%20107.png)
    
- Balanced Binary Tree
    
    heights of the two subtrees of any node differ by at most one
    for every node (height(left) - height(right) <= 1)
    
    ![image.png](image%20108.png)
    
    ![image.png](image%20109.png)
    
- Degenerate Tree / Skewed Tree
    
     nodes are arranged in a single path leaning to the right or left. Every node has single children. The tree resembles a linked list in its structure where each node points to the next node in a linear fashion.
    
    ![image.png](image%20110.png)
    

# Basics

- Implement Binary Tree
    
    ```cpp
    class Node {
        public: 
            int val;
            Node* left;
            Node* right;
    
        Node (int val) {
            this->val = val;
            this->left = NULL;
            this->right = NULL;
        }
    };
    
    Node* inputBtree() {
        int val;
        cin >> val;
        Node* root;
      
      	if (val == -1)
          root = NULL;
      	else 
          root = new Node(val);
      
        queue<Node*> q;
        if (root) q.push(root);
    
        while(!q.empty()) {
            Node* p = q.front();
            q.pop();
    
            int l, r;
            cin >> l >> r;
            
            if (l == -1) p->left = NULL;
            else p->left = new Node(l);
            if (r == -1) p->right = NULL;
            else p->right = new Node(r);
    
            if (p->left) q.push(p->left);
            if (p->right) q.push(p->right);
        }
        return root;
    }
    
    int main () {
    		// manual input
      	Node *root = new Node(10);
      	Node *a = new Node(20);
      	Node *b = new Node(30);
      
      	root->left = a;
      	root->right = b;
      
      	// automatic input
        Node* root = createBtree();
        return 0;
    }
    ```
    

# Traversals

- https://leetcode.com/problems/binary-tree-preorder-traversal/
    
    ![image.png](image%20111.png)
    
    ```cpp
    // O(n) O(n)
    // recursive
    void preOrder(Node* root) {
        if (root == NULL) return;
        cout << root->val << " ";
        preOrder(root->left);
        preOrder(root->right);
    }
    
    // iterative
    vector<int> preorderTraversal(Node* root) {
        vector<int> preorder;
        if(root == nullptr) 
            return preorder;
        
        stack<Node*> st;
        st.push(root);
        while(!st.empty()) {
            root = st.top();
            st.pop();
            preorder.push_back(root->val);
    
            if(root->right != nullptr) 
                st.push(root->right);
            
            if(root->left != nullptr) 
                st.push(root->left);
            
        }
        return preorder;
    }
    ```
    
- https://leetcode.com/problems/binary-tree-inorder-traversal/
    
    ![image.png](image%20112.png)
    
    ```cpp
    // O(n) O(n)
    // recursive
    void inOrder(Node* root) {
        if (root == NULL) return;
        inOrder(root->left);
        cout << root->val << " ";
        inOrder(root->right);
    }
    
    // iterative
    vector<int> inorderTraversal(Node* root) {
        vector<int> inorder;
        if(root == nullptr) return inorder;
        
        stack<Node*> st;
        
        while(root != nullptr || !st.empty()) {
            // Go to the leftmost node
            while(root != nullptr) {
                st.push(root);
                root = root->left;
            }
            
            // Current must be nullptr, pop from stack
            root = st.top();
            st.pop();
            inorder.push_back(root->val);
            
            // Visit right subtree
            root = root->right;
        }
        
        return inorder;
    }
    
    ```
    
- https://leetcode.com/problems/binary-tree-postorder-traversal/
    
    ![image.png](image%20113.png)
    
    ![image.png](image%20114.png)
    
    ```cpp
    // O(n) O(n)
    void postOrder(Node* root) {
        if (root == NULL) return;
        postOrder(root->left);
        postOrder(root->right);
        cout << root->val << " ";
    }
    
    // iterative (two stacks)
    vector<int> postorderTraversal(Node* root) {
        vector<int> postorder;
        if(root == nullptr) return postorder;
        
        stack<Node*> st1, st2;
        st1.push(root);
        
        while(!st1.empty()) {
            root = st1.top();
            st1.pop();
            st2.push(root);
            
            if(root->left != nullptr) st1.push(root->left);
            if(root->right != nullptr) st1.push(root->right);
        }
        
        while(!st2.empty()) {
            postorder.push_back(st2.top()->val);
            st2.pop();
        }
        
        return postorder;
    }
    
    // iterative (one stack)
    vector<int> postorderTraversalOneStack(Node* root) {
        vector<int> postorder;
        if(root == nullptr) return postorder;
        
        stack<Node*> st;
        Node* lastVisited = nullptr;
        
        while(root != nullptr || !st.empty()) {
            if(root != nullptr) {
                st.push(root);
                root = root->left;
            } else {
                Node* peekNode = st.top();
                // If right child exists and hasn't been processed yet
                if(peekNode->right != nullptr && lastVisited != peekNode->right) {
                    root = peekNode->right;
                } else {
                    postorder.push_back(peekNode->val);
                    lastVisited = st.top();
                    st.pop();
                }
            }
        }
        
        return postorder;
    }
    
    // using reverse of modified preorder
    vector<int> postorderTraversalReverse(Node* root) {
        vector<int> postorder;
        if(root == nullptr) return postorder;
        
        stack<Node*> st;
        st.push(root);
        
        while(!st.empty()) {
            root = st.top();
            st.pop();
            postorder.push_back(root->val);
            
            // Note: Push left first, then right (opposite of preorder)
            if(root->left != nullptr) st.push(root->left);
            if(root->right != nullptr) st.push(root->right);
        }
        
        // Reverse the result to get postorder
        reverse(postorder.begin(), postorder.end());
        return postorder;
    }
    ```
    
- preInPost in one
    
    ![image.png](image%20115.png)
    
    ```cpp
    // O(3n) O(4n)
    vector<vector<int>> preInPostTraversal(Node* root) {
        vector<int> pre, in, post;
        if (root == NULL) 
            return {};
    
        // Stack to maintain nodes
        // and their traversal state
        stack<pair<Node*, int>> st;
    
        // Start with the root node
        // and state 1 (preorder)
        st.push({root, 1});
    
        while (!st.empty()) {
            auto it = st.top();
            st.pop();
    
            // this is part of pre
            if (it.second == 1) {
                // Store the node's data
                // in the preorder traversal
                pre.push_back(it.first->data);
                // Move to state 2
                // (inorder) for this node
                it.second = 2;
                // Push the updated state
                // back onto the stack
                st.push(it); 
    
                // Push left child onto
                // the stack for processing
                if (it.first->left != NULL) {
                    st.push({it.first->left, 1});
                }
            }
    
            // this is a part of in
            else if (it.second == 2) {
                // Store the node's data
                // in the inorder traversal
                in.push_back(it.first->data);
                // Move to state 3
                // (postorder) for this node
                it.second = 3;
                // Push the updated state
                // back onto the stack
                st.push(it); 
    
                // Push right child onto
                // the stack for processing
                if (it.first->right != NULL) {
                    st.push({it.first->right, 1});
                }
            }
    
            // this is part of post
            else {
                // Store the node's data
                // in the postorder traversal
                post.push_back(it.first->data);
            }
        }
    
        // Returning the traversals
        vector<vector<int>> result;
        result.push_back(pre);
        result.push_back(in);
        result.push_back(post);
        return result;
    }
    
    ```
    
- https://leetcode.com/problems/binary-tree-level-order-traversal/
    
    ![image.png](image%20116.png)
    
    ![image.png](image%20117.png)
    
    ```cpp
    // O(n) O(n)
    vector<vector<int>> levelOrder(Node* root) {
      vector<vector<int>> ans;
      if (!root) return ans;
    
      queue<Node*> q;
      q.push(root);
      while(!q.empty()) {
        int size = q.size();
        vector<int> level(size);
        for (int i=0; i<size; i++) {
          TreeNode* node = q.front();
          q.pop();
          level.push_back(node->val);
          if (node->left) q.push(node->left);
          if (node->right) q.push(node->right);
        }
        ans.push_back(level);            
      }
      return ans;
    }
    // time - O(n)
    // space - O(n)
    ```
    
- https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/
    
    ![image.png](image%20118.png)
    
    ![image.png](image%20119.png)
    
    ```cpp
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
      vector<vector<int>> ans;
      if (!root) return ans;
    
      queue<TreeNode*> q;
      q.push(root);
      bool ltr = true;
      
      while(!q.empty()) {
        int size = q.size();
        vector<int> level(size);
        for (int i=0; i<size; i++) {
          TreeNode* node = q.front();
          q.pop();
          
          int index = ltr ? i : (size-i-1);
          level[index] = node->val;
          
          if (node->left) q.push(node->left);
          if (node->right) q.push(node->right);
        }
        ltr = !ltr;
        ans.push_back(level);            
      }
      return ans;
    }
    // time - O(n)
    // space - O(n)
    ```
    
- boundary traversal
    
    ![image.png](image%20120.png)
    
    ![image.png](image%20121.png)
    
    ![image.png](image%20122.png)
    
    ![image.png](image%20123.png)
    
    ![image.png](image%20124.png)
    
    ![image.png](image%20125.png)
    
    ```cpp
    // O(n) O(h)
    bool isLeaf(Node* root) {
        return !root->left && !root->right;
    }
    
    void addLeftBoundary(Node* root, vector<int> &ans) {
      Node* cur = root->left;
      while (cur) {
        if (!isLeaf(cur)) ans.push_back(cur->data);
        if (cur->left) cur = cur->left;
        else cur = cur->right;
      }
    }
    
    void addRightBoundary(Node* root, vector<int> &ans) {
      Node* cur = root->right;
      vector<int> tmp;
      
      while(cur) {
        if (!isLeaf(cur)) tmp.push_back(cur->data);
        if (cur->right) cur = cur->right;
        else cur = cur->left;
      }
      
      for (int i=tmp.size()-1; i>=0; --i) 
        ans.push_back(tmp[i]);
    }
    
    void addLeaves(Node* root, vector<int> &ans) {
      if (isLeaf(root)) {
        ans.push_back(root->data);
        return;
      }
      if (root->left) addLeaves(root->left, ans);
      if (root->right) addLeaves(root->right, ans);
    }
    
    vector<int> printBoundary(Node* root) {
      vector<int> ans;
      if (!root) return ans;
      if (!isLeaf(root)) ans.push_back(root->data);
      
      addLeftBoundary(root, ans);
      addLeaves(root, ans);
      addRightBoundary(root, ans);
      
      return ans;
    }
    // time - O(n)
    // space - O(n)
    ```
    
- https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/
    
    ![image.png](image%20126.png)
    
    ![image.png](image%20127.png)
    
    ```cpp
    // O(N * log2N * log2N * log2N) O(N + N/2)
    // two nested maps O(log2N)*O(log2N)
    // Multiset O(log2N)
    // Postorder Traversal performed using BFS as a time complexity of O(N) 
    vector<vector<int>> verticalTraversal(TreeNode* root) {
      map <int, map<int, multiset<int>>> nodes;
      queue <pair<TreeNode*, pair<int, int>>> q;
      q.push({root, {0, 0}});
      
      while (!q.empty()) {
        auto p = q.front();
        q.pop();
        
        TreeNode* node = p.first;
        int x = p.second.first, y = p.second.second;
        
        nodes[x][y].insert(node->val);
        
        if (node->left)
          q.push({node->left, {x - 1, y + 1}});
        if (node->right)
          q.push({node->right, {x + 1, y + 1}});
      }
      
      vector<vector<int>> ans;
      for (auto p : nodes) {
        vector<int> col;
        for (auto q : p.second) {
          col.insert(col.end(), q.second.begin(), q.second.end());
        }
        ans.push_back(col);
      }
      return ans;
    }
    // time - O(n)
    // space - O(n)
    ```
    
- top view
    
    ![image.png](image%20128.png)
    
    ![image.png](image%20129.png)
    
    ```cpp
    vector<int> topView(Node* root) {
      vector<int> ans;
      if (!root) return ans;
      
      map<int, int> mp;
      queue<pair<Node*, int>> q;
      q.push({root, 0});
      
      while(!q.empty()) {
        auto [node, line] = q.front();
        q.pop();
        
        if(mp.find(line) == mp.end()) mp[line] = node->data;
        if(node->left) q.push({node->left, line-1});
        if(node->right) q.push({node->right, line+1});
      }
      
      for(auto it: mp) {
        ans.push_back(it.second);
      }
      return ans;
    }
    // time - O(n)
    // space - O(n)
    ```
    
- bottom view
    
    ![image.png](image%20130.png)
    
    ![image.png](image%20131.png)
    
    ```cpp
    vector<int> bottomView(Node* root) {
      vector<int> ans;
      if (!root) return ans;
      
      map<int, int> mp;
      queue<pair<Node*, int>> q;
      q.push({root, 0});
      
      while(!q.empty()) {
        auto [node, line] = q.front();
        q.pop();
        
        mp[line] = node->data;
        
        if(node->left) q.push({node->left, line-1});
        if(node->right) q.push({node->right, line+1});
      }
      for(auto it: mp) {
        ans.push_back(it.second);
      }
      return ans;
    }
    // time - O(n)
    // space - O(n)
    ```
    
- https://leetcode.com/problems/binary-tree-right-side-view/
    
    ```cpp
    // brute force O(n) O(n)
    vector<int> rightsideView(Node* root) {
        vector<int> res;
        vector<vector<int>> levelTraversal = levelOrder(root);
    
        for (auto level : levelTraversal) 
            res.push_back(level.back());
    
        return res;
    }
    
    vector<vector<int>> levelOrder(Node* root) {
      vector<vector<int>> ans;
      if (!root) return ans;
    
      queue<Node*> q;
      q.push(root);
      while(!q.empty()) {
        int size = q.size();
        vector<int> level(size);
        for (int i=0; i<size; i++) {
          TreeNode* node = q.front();
          q.pop();
          level.push_back(node->val);
          if (node->left) q.push(node->left);
          if (node->right) q.push(node->right);
        }
        ans.push_back(level);            
      }
      return ans;
    }
    
    // O(logn) O(logn)
    void helper(Node* root, int level, vector<int> &ans) {
      if(!root) return;
      if (level == ans.size()) ans.push_back(root->val);
      helper(root->right, level+1, ans);
      helper(root->left, level+1, ans);
    }
    
    vector<int> rightSideView(Node* root) {
      vector<int> ans;
      if (!root) return ans;
      helper(root, 0, ans);
      return ans;
    }
    ```
    
- left view
    
    ```cpp
    // brute force O(n) O(n)
    vector<int> leftsideView(Node* root) {
        vector<int> res;
        vector<vector<int>> levelTraversal = levelOrder(root);
    
        for (auto level : levelTraversal) {
            res.push_back(level.front());
        }
    
        return res;
    }
    
    vector<vector<int>> levelOrder(Node* root) {
      vector<vector<int>> ans;
      if (!root) return ans;
    
      queue<Node*> q;
      q.push(root);
      while(!q.empty()) {
        int size = q.size();
        vector<int> level(size);
        for (int i=0; i<size; i++) {
          TreeNode* node = q.front();
          q.pop();
          level.push_back(node->val);
          if (node->left) q.push(node->left);
          if (node->right) q.push(node->right);
        }
        ans.push_back(level);            
      }
      return ans;
    }
    
    // O(logn) O(logn)
    void helper(Node* root, int level, vector<int> &ans) {
      if(!node) return;
      if (level == ans.size()) ans.push_back(root->val);
      helper(root->left, level+1, ans);
      helper(root->right, level+1, ans);
    }
    
    vector<int> leftView(Node* root) {
      vector<int> ans;
      if (!root) return ans;
      helper(root, 0, ans);
      return ans;
    }
    // tc - O(n)
    // space - O(h)
    
    ```
    

# Problems

- https://leetcode.com/problems/maximum-depth-of-binary-tree/
    
    ```cpp
    int maxHeight(Node *root) {
      if (root == NULL) 
        return 0;
      int l = maxHeight(root->left);
      int r = maxHeight(root->right);
      return max(l, r) + 1;
    }
    // time - O(n)
    // space - O(n)
    ```
    
- https://leetcode.com/problems/balanced-binary-tree/
    
    ```cpp
    // brute force O(n^2) calculation is performed for each node O(1)
    bool isBalanced(Node* root) {
        if (root == nullptr) 
            return true;
        
        int leftHeight = maxHeight(root->left);
        int rightHeight = maxHeight(root->right);
    
        // Check if the absolute difference in heights
        // of left and right subtrees is <= 1
        if (abs(leftHeight - rightHeight) <= 1 &&
            isBalanced(root->left) &&
            isBalanced(root->right)) {
            return true;
        }
    
        // If any condition fails, the tree is unbalanced
        return false;
    }
    
    // Function to calculate the height of a subtree
    int maxHeight(Node *root) {
      if (root == NULL) 
        return 0;
      int l = maxHeight(root->left);
      int r = maxHeight(root->right);
      return max(l, r) + 1;
    }
    
    // optimal O(n) This complexity arises from visiting each node exactly once during the postorder traversal. O(1)
    bool isBalanced(Node* root) {
        return dfsHeight(root) != -1;
    }
    
    int dfsHeight(Node* root) {
        if (root == NULL) return 0;
    
        int leftHeight = dfsHeight(root->left);
        if (leftHeight == -1) 
            return -1;
    
        int rightHeight = dfsHeight(root->right);
        if (rightHeight == -1) 
            return -1;
            
        if (abs(leftHeight - rightHeight) > 1)  
            return -1;
            
        return max(leftHeight, rightHeight) + 1;
    }
    ```
    
- https://leetcode.com/problems/diameter-of-binary-tree/
    
    ```cpp
    // optimal O(n) O(h)
    int diameterOfBinaryTree(Node* root) {
        int diameter = 0;
        height(root, diameter);
        return diameter;
    }
    
    int height(Node* node, int& diameter) {
        if (!node) {
            return 0;
        }
    
        int lh = height(node->left, diameter);
        int rh = height(node->right, diameter);
    
        diameter = max(diameter, lh + rh);
    
        return 1 + max(lh, rh);
    }
    ```
    
- https://leetcode.com/problems/binary-tree-maximum-path-sum/
    
    ```cpp
    // O(n) O(h)
    int helper(TreeNode* root, int& maxVal) {
        if (!root) return 0;
    
        int leftSum = max(0, helper(root->left, maxVal));
        int rightSum = max(0, helper(root->right, maxVal));
        maxVal = max(maxVal, root->val + leftSum + rightSum);
    
        return root->val + max(leftSum, rightSum);
    }
    int maxPathSum(TreeNode* root) {
        int maxVal = INT_MIN;
        helper(root, maxVal);
        return maxVal;
    }
    ```
    
- https://leetcode.com/problems/same-tree/
    
    ```cpp
    // O(n+m) O(h)
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (!p || !q) return p == q;
        return (p->val == q->val) 
            && isSameTree(p->left, q->left) 
            && isSameTree(p->right, q->right);
    }
    ```
    
- https://leetcode.com/problems/symmetric-tree/
    
    ```cpp
    // O(n) O(h)
    bool helper(TreeNode* left, TreeNode* right) {
        if (!left || !right) return left == right;
        if (left->val != right->val) return false;
        return helper(left->left, right->right) 
            && helper(left->right, right->left); 
    }
    
    bool isSymmetric(TreeNode* root) {
        return root == NULL || helper(root->left, root->right);
    }
    ```
    
- count tree nodes
    
    ```cpp
    int countTreeNodes(Node* root) {
        if (!root) return 0;
        return countTreeNodes(root->left) + countTreeNodes(root->right) + 1;
    }
    ```
    
- Count leaf nodes
    
    ```cpp
    int countLeafNodes(Node* root) {
        if (!root) return 0;
        if (!root->left && !root->right) return 1;
        return countLeafNodes(root->left) + countLeafNodes(root->right);
    }
    ```
    
- [Root to Node Path in Binary Tree](https://takeuforward.org/data-structure/print-root-to-node-path-in-a-binary-tree/)
    
    ```cpp
    // O(n) O(h)
    bool getPath(TreeNode* root, vector<int>& arr, int x) {
        if (!root) 
            return false;
    
        arr.push_back(root->val);
    
        if (root->val == x) 
            return true;
        
        if (getPath(root->left, arr, x)
            || getPath(root->right, arr, x)) {
            return true;
        }
    
        arr.pop_back();
        return false;
    }
    
    vector<int> solve(TreeNode* A, int B) {
        vector<int> arr;
    
        if (A == NULL) 
            return arr;
       
        getPath(A, arr, B);
        return arr;
    }
    ```
    
- https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/
    
    ```cpp
    // O(n) O(n)
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (root == NULL || root == p || root == q) {
            return root;
        }
        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);
    
        if(left == NULL) {
            return right;
        }
        else if(right == NULL) {
            return left;
        }
        else { //both left and right are not null, we found our result
            return root;
        }
    }
    ```
    
- https://leetcode.com/problems/maximum-width-of-binary-tree/
    
    ![image.png](image%20132.png)
    
    ```cpp
    // O(n) O(n)
    int widthOfBinaryTree(TreeNode* root) {
        if (!root) 
            return 0;
    
        long long ans = 0;
        queue<pair<TreeNode*, long long>> q;
        q.push({root, 0});
    
        while (!q.empty()) {
            long long size = q.size();
            long long mmin = q.front().second;
            long long first, last;
    
            for (int i = 0; i < size; i++) {
                long long cur_id = q.front().second - mmin;
                TreeNode* node = q.front().first;
                q.pop();
    
                if (i == 0) first = cur_id;
                if (i == size - 1) last = cur_id;
    
                if (node->left) 
                    q.push({node->left, cur_id * 2 + 1});
            
                if (node->right) 
                    q.push({node->right, cur_id * 2 + 2});
            }
            ans = max(ans, last - first + 1);
        }
        return ans;
    }
    ```
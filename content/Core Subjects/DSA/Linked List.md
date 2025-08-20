---
title: Linked List
draft: false
tags: 
date: 19-Aug-2025
---
![image.png](image%2025.png)
# Singly Linked List
### implement Singly linked list
    
![image.png](image%2026.png)

![image.png](image%2027.png)

![image.png](image%2028.png)

```cpp
#include<bits/stdc++.h>
using namespace std;

class Node {
 public:
   int val;
   Node* next;

   Node(int val) {
	 this->val=val;
	 this->next=NULL;
   }
};

void insertAtHead(Node *&head, int val) {
  Node *newNode = new Node(val);
  newNode->next = head;
  head = newNode;
}

void insertAtTail(Node *&head, Node *&tail, int val) {
  Node *newNode = new Node(val);

  if (head == NULL) {
	head = newNode;
	tail = newNode;
	return;
  }

  // if tail is not considered use this code
  Node *tmp = head;
  while (tmp->next != NULL)
	tmp = tmp->next;

  tmp->next = newNode;

  // if tail is considered use this code
  tail->next = newNode;
  tail = newNode;
}

void insertAtPos(Node *&head, int val, int index) {
  Node *newNode = new Node(val);
  Node *tmp = head;

  for (int i=1; i<index; i++) {
	if (tmp == NULL) {
	  cout << "Invalid Index" << endl;
	  return;
	}
	tmp = tmp->next;
  }

  newNode->next = tmp->next;
  tmp->next = newNode;
}

void deleteHead(Node *&head) {
  if (head == NULL) {
	cout << "Linked list is empty";
	return;
  }
  Node* deleteNode = head;
  head = head->next;
  delete deleteNode;
}

void deleteTail(Node *&head) {
  if (head == NULL) {
	cout << "Linked list is empty";
	return;
  }
  if (head->next == NULL) {
	delete head;
	head = nullptr;
	return;
  }

  Node* tmp = head;
  while (tmp->next->next != NULL) {
	tmp = tmp->next;
  }
  delete tmp->next;
  tmp->next = nullptr;
}

void deleteAtPos(Node *&head, int pos) {
  Node *tmp = head;
  for (int i=1; i<pos; i++) {
	if (tmp == NULL) {
	  cout << "Invalid Index" << endl;
	  return;
	}
	if (tmp->next == NULL) {
	  cout << "Invalid Index" << endl;
	  return;
	}
	tmp = tmp->next;
  }

  Node* deleteNode = tmp->next;
  tmp->next = tmp->next->next;
  delete deleteNode;
}

int size(Node *head) {
  Node *tmp = head;
  int count = 0;

  while (tmp != NULL) {
	count++;
	tmp = tmp->next;
  }
  return count;
}

void printsll(Node* head) {
  Node* tmp = head;

  // print till last value
  while (tmp != NULL) {
	cout << tmp->val << " ";
	tmp = tmp->next;
  }

  // print till second last value
  while (tmp->next != NULL) {
	cout << tmp->val << " ";
	tmp = tmp->next;
  }
}

void printRecursionSll(Node *head) {
  if (head == NULL) return;
  cout << head->val << " ";
  printReverseSll(head->next);
}

void printReverseSll(Node *head) {
  if (head == NULL) return;
  printReverseSll(head->next);
  cout << head->val << " ";
}

void sortSll(Node *&head) {
  for (Node *i = head; i->next != NULL; i = i->next) {
	for (Node *j = i->next; j != NULL; j = j->next) {
	  if (i->val > j->val)
		swap(i-val, j->val);
	}
  }
}

int main() {
 // static object
 Node a(10); // এখানে a object এ 10 value এর একটা node create করছি।
 Node b(20); // এখানে b object এ 20 value এর একটা node create করছি।
 a.next=&b; //এখানে b node এর address a এর next/pointer এ রাখা হচ্ছে। যাতে a দিয়ে b কে access করা যায়।

 cout<<a.val<<endl; // এখানে a এর value print করে দেখলাম।
 cout<<b.val<<endl; // এখানে b এর value print করে দেখলাম।
 cout<<(*a.next).val<<endl; // এখানে b এর value a কে dereference করে print করে দেখলাম।
 cout<<a.next->val<<endl; // এখানে b এর value a কে অন্যভাবে dereference করে print করে দেখলাম।

 // dynamci object
 Node* head = new Node(10);
 Node* a = new Node(20);
 Node* b = new Node(30);
 Node* c = new Node(40);
 Node *tail = c;

 head->next = a;
 a->next = b;
 b->next = c;

 cout << head->val;
 cout << a->val;
 cout << head->next->val;

  // taking input
  Node *head = NULL; //head initialize করা হচ্ছে।
  Node *tail = NULL; //tail initialize করা হচ্ছে।
  int val;
  while (true) // একটা infinity while loop চালানো হচ্ছে।
  {
	cin >> val; // একটা value input নেয়া হচ্ছে।
	if (val == -1){  //check করা হচ্ছে value টা -1 কিনা।
	  break; // value -1 হলে loop break করা হচ্ছে।
	}
	insertAtTail(head, tail, val); //যেহেতু আমরা generally একটার পর একটা value insert করি তাই insert_tail function call করা হচ্ছে।
  }

 printsll(head);
 insertAtTail(head, tail, 1);
 return 0;
}

```

```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

# Implementation for Singly Linked List
class LinkedList:
    def __init__(self):
        # Init the list with a 'dummy' node which makes 
        # removing a node from the beginning of list easier.
        self.head = ListNode(-1)
        self.tail = self.head
    
    def insertEnd(self, val):
        self.tail.next = ListNode(val)
        self.tail = self.tail.next

    def remove(self, index):
        i = 0
        curr = self.head
        while i < index and curr:
            i += 1
            curr = curr.next
        
        # Remove the node ahead of curr
        if curr:
            curr.next = curr.next.next

    def print(self):
        curr = self.head.next
        while curr:
            print(curr.val, ' -> ')
            curr = curr.next
        print()
```
- Singly Linked list all operations complexity analysis
	- আমরা টেল ট্র্যাক রাখি তাহলে কোন লুপ চালাতে হয় না। কমপ্লেক্সিটি 0(1)। যদি টেল ট্র্যাক না রাখি তাহলে লুপ চালিয়ে টেল পর্যন্ত যেতে হয়। তখন কমপ্লেক্সিটি 0(N)
	- ইনসার্ট এট এনি পজিশনঃ *লুপ চালিয়ে পজিশন পর্যন্ত যেতে হয়। কমপ্লেক্সিটি 0(N)।
	- ডিলিট হেডঃ *কোন লুপ চালাতে হয় না। কমপ্লেক্সিটি 0(1)
	- ডিলিট টেলঃ *যদি আমরা টেল ট্র্যাক রাখি তাহলেও লুপ চালাতে হবে কারন টেলকে পিছিয়ে নিয়ে আসা যায় না। তাই আগে লুপ চালিয়ে লাস্ট এর আগের নোড পর্যন্ত যেতে হবে তারপর টেল ডিলিট করতে হবে। কমপ্লেক্সিটি 0(N)।
	- ডিলিট এট এনি পজিশনঃ *লুপ চালিয়ে পজিশন পর্যন্ত যেতে হয়। কমপ্লেক্সিটি 0(N)।

![image.png](image%2029.png)

# Doubly Linked List
### implement Doubly linked list
![image.png](image%2030.png)

```cpp
// doubly linked list
class Node {
	public:
		int val;
		Node* next;
		Node* prev;

	Node (int val) {
		this->val = val;
		this->next = NULL;
		this->prev = NULL;
	}
};

void insertHead(Node *&head, Node* &tail, int val) {
  Node *newNode = new Node(val);
  if (head == NULL) {
	head = newNode;
	tail = newNode;
	return;
  }
  newNode->next = head;
  head->prev = newNode;
  head = newNode;
}

void insertTail(Node *&head, Node* &tail, int val) {
  Node *newNode = new Node(val);
  if (tail == NULL) {
	head = newNode;
	tail = newNode;
	return;
  }
  tail->next = newNode;
  newNode->prev = tail;
  tail = newNode;
}

void insertAtPos(Node *head, int pos, int val) {
  Node *newNode = new Node(val);

  Node *tmp = head;
  for (int i=1; i<pos; i++)
	tmp = tmp->next;

  newNode->next = tmp->next;
  tmp->next = newNode;
  newNode->next->prev = newNode;
  newNode->prev = tmp;
}

void create_dll (Node* &head, Node* &tail, int val, int pos, int index) {
	Node* newNode = new Node(val);
	if (!head) {
		head = newNode;
		tail = newNode;
		return;
	}
	if (pos == 0) {
		newNode->next = head;
		head->prev = newNode;
		head = newNode;
		return;
	}
	if (pos == index+1) {
		tail->next = newNode;
		newNode->prev = tail;
		tail = newNode;
		return;
	}
	Node* p = head;
	pos--;
	while (pos--) {
		p = p->next;
	}
	newNode->next = p->next;
	newNode->prev = p;
	p->next = newNode;
	newNode->next->prev = newNode;
}

void deleteHead(Node *&head, Node *&tail) {
  Node *deleteNode = head;
  head = head->next;
  delete deleteNode;
  head->prev = NULL;
}

void deleteTail(Node *&head, Node* &tail) {
  Node *deleteNode = tail;
  tail = tail->prev;
  delete deleteNode;
  tail->next = NULL;
}

void deleteAtPos(Node *head, int pos) {
  Node *tmp = head;
  for (int i=1; i<pos; i++)
	tmp = tmp->next;
  Node *deleteNode = tmp->next;
  tmp->next = tmp->next->next;
  tmp->next->prev = tmp;
  delete deleteNode;
}

int size(Node *head) {
  Node *tmp = head;
  int count = 0;

  while(tmp != NULL) {
	count++;
	tmp = tmp->next;
  }
  return count;
}

void printDll(Node *head) {
  Node *tmp = head;
  while(tmp != NULL) {
	cout << tmp->val;
	tmp = tmp->next;
  }
}

void printReverseDll(Node *tail) {
  Node *tmp = tail;
  while (tmp != NULL) {
	cout << tmp->val;
	tmp = tmp->prev;
  }
}

int main() {
  Node *head = new Node(10);
  Node *a = new Node(20);
  Node *b = new Node(30);
  Node *tail = b;

  head->next = a;
  a->prev = head;
  a->next = b;
  b->prev = a;

  // taking input
  Node *head = NULL; //head initialize করা হচ্ছে।
  Node *tail = NULL; //tail initialize করা হচ্ছে।
  int val;
  while (true) // একটা infinity while loop চালানো হচ্ছে।
  {
	cin >> val; // একটা value input নেয়া হচ্ছে।
	if (val == -1){  //check করা হচ্ছে value টা -1 কিনা।
	  break; // value -1 হলে loop break করা হচ্ছে।
	}
	insert_tail(head, tail, val); //যেহেতু আমরা generally একটার পর একটা value insert করি তাই insert_tail function call করা হচ্ছে।
  }

  int pos;
  cin >> pos;

  if (pos > size(head))
	cout << "Invalid" << endl;
  else if (pos == 0)
	insert_head(head, tail, val);
  else if (pos == size(head))
	insert_tail(head, tail, val);
  else
	insert_at_position(head, pos, val);

  return 0;
}

```

```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None
        self.prev = None

# Implementation for Doubly Linked List
class LinkedList:
    def __init__(self):
        # Init the list with 'dummy' head and tail nodes which makes 
        # edge cases for insert & remove easier.
        self.head = ListNode(-1)
        self.tail = ListNode(-1)
        self.head.next = self.tail
        self.tail.prev = self.head
    
    def insertFront(self, val):
        newNode = ListNode(val)
        newNode.prev = self.head
        newNode.next = self.head.next

        self.head.next.prev = newNode
        self.head.next = newNode

    def insertEnd(self, val):
        newNode = ListNode(val)
        newNode.next = self.tail
        newNode.prev = self.tail.prev

        self.tail.prev.next = newNode
        self.tail.prev = newNode

    # Remove first node after dummy head (assume it exists)
    def removeFront(self):
        self.head.next.next.prev = self.head
        self.head.next = self.head.next.next

    # Remove last node before dummy tail (assume it exists)
    def removeEnd(self):
        self.tail.prev.prev.next = self.tail
        self.tail.prev = self.tail.prev.prev

    def print(self):
        curr = self.head.next
        while curr != self.tail:
            print(curr.val, " -> ")
            curr = curr.next
        print()
```

![image.png](image%2031.png)

- Insert at head: এই Task এ array তে সবচেয়ে বেশি complexity লাগছে, কারণ array এর ক্ষেত্রে আমাদের বাকি সব valueকে অন্য position এ নিয়ে তারপর head এ value insert করতে হয়। অন্যদিকে singly and doubly linked list এ head node এর সাথে new node এর connection create করলেই হয়ে যায়।
- Insert at tail: এইক্ষেত্রে কোনো value shift করতে হচ্ছে না just last এ add করতে হচ্ছে তাই সবক্ষেত্রে same complexity কাজ করছে।
- Insert at position: এখানে 3 টা data structure এই same O(n) আসে। কারণ প্রতিবার আমাদের একটা নির্দিষ্ট position এ অব্দি loop চালাতে হচ্ছে।
- Delete head: singly ও doubly linked list এ head track রাখা যায় আর delete করা মানে head এ যে node আছে সেটা disconnect করে দেয়া মূলত, তাই এদের বেলায় O(1) complexity. আর array এর বেলায় delete head এ কোনো value delete করতে হলে পরের value গুলোর position shift করতে হবে, তাই array এর জন্য O(n) complexity আসে।
- Delete tail: এখানে array এবং doubly linked list এ শেষ position টা আমরা track রাখতে পারি বা সহজে access করতে পারি, তাই শেষ বা tail value delete করতে আমাদের O(1) complexity হয়। কিন্তু singly linked list এর বেলায় tail track রাখা হয় না , তাই tail অব্দি যেতে আমাদের পুরো list ঘুরে যেতে হয়। তাই এর tail delete করার জন্য আমাদের singly list এর জন্য O(n) complexity আসে।
- Delete at position: insert এর মতো delete এর বেলায় ও ঠিক একই logic এর জন্য এই 3 data structure (array, signly linked list and doubly linked list) এর জন্য O(n) complexity পাওয়া যাচ্ছে।
### [146. LRU Cache](https://leetcode.com/problems/lru-cache/)   
```python
# brute force O(n) for each put()put() and get()get() operation. O(n)
class LRUCache:
    def __init__(self, capacity: int):
        self.cache = []
        self.capacity = capacity

    def get(self, key: int) -> int:
        for i in range(len(self.cache)):
            if self.cache[i][0] == key:
                tmp = self.cache.pop(i)
                self.cache.append(tmp)
                return tmp[1]
        return -1

    def put(self, key: int, value: int) -> None:
        for i in range(len(self.cache)):
            if self.cache[i][0] == key:
                tmp = self.cache.pop(i)
                tmp[1] = value
                self.cache.append(tmp)
                return

        if self.capacity == len(self.cache):
            self.cache.pop(0)
            
        self.cache.append([key, value])

# Doubly Linked List O(1) for each put()put() and get()get() operation. O(n)
class Node:
    def __init__(self, key, val):
        self.key, self.val = key, val
        self.prev = self.next = None

class LRUCache:
    def __init__(self, capacity: int):
        self.cap = capacity
        self.cache = {}  # map key to node

        self.left, self.right = Node(0, 0), Node(0, 0)
        self.left.next, self.right.prev = self.right, self.left

    def remove(self, node):
        prev, nxt = node.prev, node.next
        prev.next, nxt.prev = nxt, prev

    def insert(self, node):
        prev, nxt = self.right.prev, self.right
        prev.next = nxt.prev = node
        node.next, node.prev = nxt, prev

    def get(self, key: int) -> int:
        if key in self.cache:
            self.remove(self.cache[key])
            self.insert(self.cache[key])
            return self.cache[key].val
        return -1

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            self.remove(self.cache[key])
        self.cache[key] = Node(key, value)
        self.insert(self.cache[key])

        if len(self.cache) > self.cap:
            lru = self.left.next
            self.remove(lru)
            del self.cache[lru.key]

# Built-In Data Structure O(1) for each put()put() and get()get() operation. O(n)
class LRUCache:

    def __init__(self, capacity: int):
        self.cache = OrderedDict()
        self.cap = capacity

    def get(self, key: int) -> int:
        if key not in self.cache:
            return -1
        self.cache.move_to_end(key)
        return self.cache[key]

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            self.cache.move_to_end(key)
        self.cache[key] = value

        if len(self.cache) > self.cap:
            self.cache.popitem(last=False)
```
# Fast and Slow Pointer
### Find the middle of a linked list with two pointers   
```python
# Time: O(n), Space: O(1)
def middleOfList(head):
    slow, fast = head, head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    return slow
```
### Determine if the linked list contains a cycle
```python
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
### Determine if the linked list contains a cycle and return the beginning of the cycle, otherwise return null 
```python
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
# Circular Linked List

- Implement Circular Linked List
    
    ![image.png](image%2032.png)
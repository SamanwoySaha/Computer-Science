---
title: Python
draft: false
tags: 
date: 10-Aug-2025
---
# Reference
# Creating environment variable
## 1
```bash
python -m venv myenv  
source myenv/bin/activate
deactivate
```
## 2
```bash
virtualenv -p python3 virtual_env
source virtual_env/bin/activate
deactivate 
```
## 3
```bash
conda create -p venv python==3.10 -y
conda activate absolute_path_to_venv 
conda deactivate
```

# Basic Syntax and Structure
## Variables
```python
## Case sensitivity- Python is case sensitive
name = "Krish"
age = 32
print(name) # Krish

type("type:", name) # type: str
print(type(name)) # <class 'str'>
type(age) # int
print(type(age)) # <class 'int'>

## Multiple Statements on a single line
x = 5; y = 10; z = x + y
print(z) # 15

# Line Continuation: Use a backslash (\) to continue a statement to the next line
total = 1+2+3+4+5+6+7+\
4+5+6
print(total) # 43

grades = [85, 92, 78, 90, 88]
average_grade = sum(grades) / len(grades)
print(f"Average Grade: {average_grade:.2f}") # Average Grade: 88.00
```
## input
```python
age=int(input("What is the age")) # prompt appears to take input, let say 23
print(age, type(age)) # 23 <class 'int'>
```
## Data Types
- Python is dynamically typed,type of a variable is determined at runtime
- Advanced Data Types
	- Lists
	- Tuples
	- Sets
	- Dictionaries
### List
- Lists are ordered, mutable collections of items.
- They can contain items of different data types.
```python
lst=list()
print(type(lst)) # <class 'list'>

print(list((1,2,3,4,5,6))) # [1, 2, 3, 4, 5, 6]

names=["Krish","Jack","Jacob",1,2,3,4,5]

print(type(name)) # <class 'list'>
print(names) # ['Krish', 'Jack', 'Jacob', 1, 2, 3, 4, 5]

print(names[0]) # Krish
print(names[-1]) # 5 (last item)
names[1]="Sam"
print(names) # ['Krish', 'Sam', 'Jacob', 1, 2, 3, 4, 5]
names[1:]="watermelon"
print(names) # ['Krish', 'w', 'a', 't', 'e', 'r', 'm', 'e', 'l', 'o', 'n']

if "Krish" in names:
	print("yes") # yes
	
## Nested List
lst=[[1,2,3,4],[6,7,8,9],[1,"Hello",3.14,"c"]]
lst[0][0:3] # [1, 2, 3]
```
#### Methods
```python
fruits=["apple","banana","cherry","kiwi","gauva"]

fruits.append("orange") ## Add an item to the end
print(fruits) # ['apple', 'banana', 'cherry', 'kiwi', 'gauva', 'orange']

fruits.insert(1,"watermelon") # insert to position
print(fruits) # ['apple', 'watermelon', 'banana', 'cherry', 'kiwi', 'gauva', 'orange']

fruits.remove("banana") ## Removing the first occurance of an item
print(fruits) # ['apple', 'watermelon', 'cherry', 'kiwi', 'gauva', 'orange']

popped_fruit=fruits.pop() # Remove and return the last element
print(popped_fruit) # orange
print(fruits) # ['apple', 'watermelon', 'cherry', 'kiwi', 'gauva']

index=fruits.index("cherry")
print(index) # 2

fruits.insert(2,"banana")
print(fruits.count("banana")) # 1
print(fruits) # ['apple', 'watermelon', 'banana', 'cherry', 'kiwi', 'gauva']

fruits.sort() # Sorts the list in ascending order
print(fruits) # ['apple', 'banana', 'cherry', 'gauva', 'kiwi', 'watermelon']

fruits.reverse() # Reverse the list
print(fruits) # ['watermelon', 'kiwi', 'gauva', 'cherry', 'banana', 'apple']

fruits.clear() ## Remove all items from the list
print(fruits) # []
```
#### Slicing
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

print(numbers[2:5]) # [3, 4, 5]
print(numbers[:5]) # [1, 2, 3, 4, 5]
print(numbers[5:]) # [6, 7, 8, 9, 10]
print(numbers[::2]) # [1, 3, 5, 7, 9]
print(numbers[::-1]) # [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
print(numbers[::-2]) # [10, 8, 6, 4, 2]
```
### Tuples
- ordered collections of items that are immutable
- similar to list, but the immutability makes them different
```python
empty_tuple=()
print(empty_tuple) # ()
print(type(empty_tuple)) # <class 'tuple'>

tpl=tuple()
print(type(tpl)) # <class 'tuple'>

numbers=tuple([1,2,3,4,5,6])
print(numbers) # (1, 2, 3, 4, 5, 6)

mixed_tuple=(1,"Hello World",3.14, True)
print(mixed_tuple) # (1, 'Hello World', 3.14, True)

print(numbers[2]) # 3
print(numbers[0:4]) # (1, 2, 3, 4)

concatenation_tuple=numbers + mixed_tuple
print(concatenation_tuple) # (1, 2, 3, 4, 5, 6, 1, 'Hello World', 3.14, True)

mixed_tuple * 3 # (1, 'Hello World', 3.14, True, 1, 'Hello World', 3.14, True, 1, 'Hello World', 3.14, True)

# packing
packed_tuple=1,"Hello",3.14
print(packed_tuple) # (1, 'Hello', 3.14)

# unpacking
numbers=(1,2,3,4,5,6)
first,*middle,last=numbers
print(first) # 1
print(middle) # [2,3,4,5]
print(last) # 6

nested_tuple = ((1, 2, 3), ("a", "b", "c"), (True, False))
print(nested_tuple[0]) # (1, 2, 3)
print(nested_tuple[1][2]) # c
```
#### Immutable nature of tuple
```python
numbers=(1,2,3,4,5,6)
numbers[1]="Krish" # TypeError: 'tuple' object does not support item assignment
print(numbers) # (1, 2, 3, 4, 5, 6)
```
#### Methods
```python
numbers=(1,2,3,4,5,6)

print(numbers.count(1)) # 1
print(numbers.index(3)) # 2
```
### Sets
- collection of unique items
- unordered
- useful for membership tests, eliminating duplicate entries, and performing mathematical set operations like union, intersection, difference, and symmetric difference.
```python
my_set={1,2,3,4,5}
print(my_set) # {1,2,3,4,5}
print(type(my_set)) # <class 'set'>

my_empty_set=set()
print(type(my_empty_set)) # <class 'set'>

my_empty_set=set([1,2,3,6,5,4,5,6])
print(my_empty_set) # {1, 2, 3, 4, 5, 6}
```
#### Methods
```python
my_set=set([1,2,3,4,5,6])
my_set.add(7)
print(my_set) # {1, 2, 3, 4, 5, 6, 7}
my_set.add(7)
print(my_set) # {1, 2, 3, 4, 5, 6, 7}

my_set.remove(3)
print(my_set) # {1, 2, 4, 5, 6, 7}

my_set.discard(11)
print(my_set) # {1, 2, 4, 5, 6, 7}

removed_element=my_set.pop()
print(removed_element) # 1
print(my_set) # {2, 4, 5, 6, 7}

my_set.clear()
print(my_set) # set()

print(4 in my_set) # True


```
#### Mathematical Operation
```python
set1={1,2,3,4,5,6}
set2={4,5,6,7,8,9}
set3={}

### Union
union_set=set1.union(set2)
print(union_set) # {1, 2, 3, 4, 5, 6, 7, 8, 9}

## Intersection
intersection_set=set1.intersection(set2)
print(intersection_set) # {4, 5, 6}

set3.intersection_update(set2)
print(set3) # {4, 5, 6}

# difference
print(set1.difference(set2)) # {1, 2, 3}

## Symmetric Difference
set1.symmetric_difference(set2) # {1, 2, 3, 7, 8, 9}

set1={1,2,3,4,5}
set2={3,4,5}
## is subset
print(set1.issubset(set2)) # False
print(set1.issuperset(set2)) # True
```
### Dictionaries
- unordered
- store data in key-value pairs
- keys must be unique and immutable (e.g., strings, numbers, or tuples)
- dictionary are mutable, so you can add, update or delete elements
- useful in counting word frequency, grouping data, storing configuration settings, managing phonebooks, tracking inventory, and caching results.
```python
## Creating Dictionaries
empty_dict={}
print(type(empty_dict)) # <class 'dict'>

empty_dict=dict()
empty_dict # {}

student={"name":"Krish","age":32,"grade":'A'}
print(student) # {"name":"Krish","age":32,"grade":24}
print(type(student)) # <class 'dict'>

## accessing Dictionary Elements
print(student['grade']) # A
print(student['age']) # 32
print(student.get('grade')) # A
print(student.get('last_name')) # Nonq
print(student.get('last_name',"Not Available")) # Not Available

# Single key is slways used
student={"name":"Krish","age":32,"name":24}
print(student) # {'name': 24, 'age': 32}

# Modifying Dictionary Elements
student["age"]=33 ##update value for the key
print(student) # {'name': 'Krish', 'age': 33, 'grade': 'A'}
student["address"]="India" ## added a new key and value
print(student) # {'name': 'Krish', 'age': 33, 'grade': 'A', 'address': 'India'}
del student['grade'] ## delete key and value pair
print(student) # {'name': 'Krish', 'age': 33, 'address': 'India'}

students={
	"student1":{"name":"Krish","age":32},
	"student2":{"name":"Peter","age":35}
}
print(students) # {'student1': {'name': 'Krish', 'age': 32}, 'student2': {'name': 'Peter', 'age': 35}}
print(students["student2"]["name"]) # Peter
students.items() # dict_items([('student1', {'name': 'Krish', 'age': 32}), ('student2', {'name': 'Peter', 'age': 35})])

dict1={"a":1,"b":2}
dict2={"b":3,"c":4}
merged_dict={**dict1,**dict2}
print(merged_dict) # {'a': 1, 'b': 3, 'c': 4}
```
#### Methods
```python
student={'name': 'Krish', 'age': 33, 'address': 'India'}

keys=student.keys() ##get all the keys
print(keys) # dict_keys(['name', 'age', 'address'])
values=student.values() ##get all values
print(values) # dict_values(['Krish', 33, 'India'])
items=student.items() ##get all key value pairs
print(items) # dict_items([('name', 'Krish'), ('age', 33), ('address', 'India')])

## shallow copy
student_copy=student
print(student) # {'name': 'Krish', 'age': 33, 'address': 'India'}
print(student_copy) # {'name': 'Krish', 'age': 33, 'address': 'India'}
student["name"]="Krish2"
print(student) # {'name': 'Krish2', 'age': 33, 'address': 'India'}
print(student_copy) # {'name': 'Krish2', 'age': 33, 'address': 'India'}

student_copy1=student.copy() ## shallow copy
print(student_copy1) # {'name': 'Krish2', 'age': 33, 'address': 'India'}
print(student) # {'name': 'Krish2', 'age': 33, 'address': 'India'}
student["name"]="KRish3"
print(student_copy1) # {'name': 'Krish2', 'age': 33, 'address': 'India'}
print(student) # {'name': 'Krish3', 'age': 33, 'address': 'India'}
```

# Operators
## Arithmetic Operator
```python
# Floor Division
a = 11; b = 5
floor_div = a // b # 2
```
## Relational / Comparison operators

```python
is # object identity
is not # negated object identity
```
## Logical operators 

```python
and # &&
or # ||
not # !
```
# Control Structures 
## Conditional Statements

## Loop
### iterate over range
```python
for i in range(3): # (start, end) default start = 0
	print(i) # 0 1 2
	
for i in range(1, 4): # (start, end)
	print(i) # 1 2 3

for i in range(1, 5, 2): # (start, end, step)
	print(i) # 1 3 

for i in range(3 ,1, -1): # (start, end, step) negative step = reverse
	print(i) # 3 2
	
for i in range(6 ,1, -2): # (start, end, step) negative step = reverse
	print(i) # 6 4 2
```
### iterate over string
```python
str="One Two"

for i in str:
	print(i) # O n e  T w o
```
### iterate over list
```python
numbers = [1, 2, 3]

# Iterating Over List
for number in numbers: 
	print(number) # 1 2 3

# Iterating with index
for index,number in enumerate(numbers):
	print(index,number) 
# 0 1
# 1 2
# 2 3

# Basic List Comphrension
lst=[]

for x in range(10):
	lst.append(x**2)
print(lst) # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

lst2=[x**2 for x in range(10)] # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# List Comprehension with Condition
lst=[]

for i in range(10):
	if i%2==0:
		lst.append(i)
print(lst) # [0, 2, 4, 6, 8]

even_numbers=[num for num in range(10) if num%2==0]
print(even_numbers) # [0, 2, 4, 6, 8]

feedback = ["Great service!", "Very satisfied", "Could be better", "Excellent experience"]
positive_feedback_count = sum(1 for comment in feedback if "great" in comment.lower() or "excellent" in comment.lower())
print(f"Positive Feedback Count: {positive_feedback_count}") # Positive Feedback Count: 2

## Nested List Comphrension
lst1=[1,2,3,4]
lst2=['a','b','c','d']
pair=[[i,j] for i in lst1 for j in lst2]
print(pair) # [[1, 'a'], [1, 'b'], [1, 'c'], [1, 'd'], [2, 'a'], [2, 'b'], [2, 'c'], [2, 'd'], [3, 'a'], [3, 'b'], [3, 'c'], [3, 'd'], [4, 'a'], [4, 'b'], [4, 'c'], [4, 'd']]

# List Comprehension with function calls
words = ["hello", "world", "python", "list", "comprehension"]
lengths = [len(word) for word in words]
print(lengths) # Output: [5, 5, 6, 4, 13]

```
### iterate over tuple
```python
nested_tuple = ((1, 2, 3), ("a", "b", "c"), (True, False))
for sub_tuple in nested_tuple:
	for item in sub_tuple:
		print(item,end=" ")
	print()
# 1 2 3 
# a b c 
# True False
```
### iterate over dictionary
```python
student={'name': 'Krish', 'age': 33, 'address': 'India'}

for keys in student.keys():
	print(keys) # name age address
	
for value in student.values():
	print(value) # Krish 33 India
	
for key,value in student.items():
	print(f"{key}:{value}") # name:Krish age:33 address:India
	
students={
	"student1":{"name":"Krish","age":32},
	"student2":{"name":"Peter","age":35}
}

for student_id,student_info in students.items():
	print(f"{student_id}:{student_info}")
	for key,value in student_info.items():
		print(f"{key}:{value}")
		
# student1:{'name': 'Krish', 'age': 32} 
# name:Krish 
# age:32 
# student2:{'name': 'Peter', 'age': 35} 
# name:Peter 
# age:35

numbers=[1,2,2,3,3,3,4,4,4,4]
frequency={}

for number in numbers:
	if number in frequency:
		frequency[number]+=1
	else:
		frequency[number]=1

print(frequency) # {1: 1, 2: 2, 3: 3, 4: 4}

## Dictionary Comphrehension
squares={x:x**2 for x in range(5)}
print(squares) # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

evens={x:x**2 for x in range(10) if x%2==0}
print(evens) # {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}
```
### Loop control statements
#### pass
```python
# pass statement is a null operation; it does nothing.
for i in range(5):
	if i==3:
		pass
	print(i)
# 0 1 2 3 4
```
# Functions
```python
def multiply(a,b):
	return a*b,a
multiply(2,3) # (6, 2)
```
## Variable Length Arguments
```python
## Positional arguments
def print_numbers(*args):
	for number in args:
		print(number)
print_numbers(1,2,"Krish") # 1 2 Krish

# Keywords Arguments
def print_details(**kwargs):
	for key,value in kwargs.items():
		print(f"{key}:{value}")
print_details(name="Krish",age="32",country="India") 
# name:Krish age:32 country:India

# both combined
def print_details(*args,**kwargs):
	for val in args:
		print(f" Positional arument :{val}")
	for key,value in kwargs.items():
		print(f"{key}:{value}")
print_details(1,2,3,4,"Krish",name="Krish",age="32",country="India")
# Positional arument :1 
# Positional arument :2 
# Positional arument :3 
# Positional arument :4 
# Positional arument :Krish 
# name:Krish 
# age:32 
# country:India
```
## Examples
```python
# Password Strength Checker
def is_strong_password(password):
	if len(password)<8:
		return False
	if not any(char.isdigit() for char in password):
		return False
	if not any(char.islower() for char in password):
		return False
	if not any(char.isupper() for char in password):
		return False
	if not any(char in '!@#$%^&*()_+' for char in password):
		return False
	return True

print(is_strong_password("WeakPwd")) # False
print(is_strong_password("Str0ngPwd!")) # True

# total cost of items in shopping cart
def calculate_total_cost(cart):
	total_cost=0
	for item in cart:
		total_cost+=item['price']* item['quantity']
	return total_cost

cart=[
	{'name':'Apple','price':0.5,'quantity':4},
	{'name':'Banana','price':0.3,'quantity':6},
	{'name':'Orange','price':0.7,'quantity':3}
]

total_cost=calculate_total_cost(cart)
print(total_cost) # 5.8999999999999995

# check palindrome
def is_palindrome(s):
	s=s.lower().replace(" ","")
	return s==s[::-1]

print(is_palindrome("A man a plan a canal Panama")) # True
print(is_palindrome("Hello")) # False

# validate email address
import re

def is_valid_email(email):
	pattern = r'^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$'
	return re.match(pattern, email) is not None

print(is_valid_email("test@example.com")) # Output: True
print(is_valid_email("invalid-email")) # Output: False

# read a file and count the frequency of each word
def count_word_frequency(file_path):
	word_count={}
	with open(file_path,'r') as file:
		for line in file:
			words=line.split()
			for word in words:
				word=word.lower().strip('.,!?;:"\'')
				word_count[word]=word_count.get(word,0)+1
	return word_count

filepath='sample.txt'
word_frequency=count_word_frequency(filepath)
print(word_frequency) # {'hello': 1, 'world': 1, 'how': 1, 'are': 1, 'you': 1, 'my': 1, 'name': 1, 'is': 1, 'krish': 2}
```
## Lambda
- anonymous functions
- can have any no of arguments but only one expression
- used for short operations or as arguments to higher-order functions
```python
#Syntax
lambda arguments: expression

# ex 1
def addition(a,b):
	return a+b
addition(2,3) # 5

addition1=lambda a,b:a+b
print(addition1(5,6)) # 11

# ex 2
def even(num):
	if num%2==0:
		return True
	return False
even(24) # True

even1=lambda num:num%2==0
even1(12) # True

# ex 3
def addition(x,y,z):
	return x+y+z
addition(12,13,14)

addition1=lambda x,y,z:x+y+z
addition1(12,13,14) # 39
```
## Maps
- applies a given function to all items in an input list (or any other iterable) and returns a map object (an iterator).
```python
numbers=[1,2,3,4,5,6]
list(map(lambda x:x**2,numbers)) # [1, 4, 9, 16, 25, 36]

def square(x):
	return x*x
square(10) # 100
list(map(square,numbers)) # [1, 4, 9, 16, 25, 36]

# multiple iterables
numbers1=[1,2,3]
numbers2=[4,5,6]
list(map(lambda x,y:x+y,numbers1,numbers2)) # [5, 7, 9]

# convert strings to integers
str_numbers = ['1', '2', '3', '4', '5']
list(map(int, str_numbers)) # [1, 2, 3, 4, 5]

# covert to upper case
words=['apple','banana','cherry']
list(map(str.upper,words)) # ['APPLE', 'BANANA', 'CHERRY']

# list of dictionary
def get_name(person):
	return person['name']

people=[
	{'name':'Krish','age':32},
	{'name':'Jack','age':33}
]
list(map(get_name,people)) # ['Krish', 'Jack']
```
## Filter
- ilter() function constructs an iterator from elements of an iterable for which a function returns true.
```python
lst=[1,2,3,4,5,6,7,8,9,10]
even=list(filter(even,lst)) # [2, 4, 6, 8, 10]
greater_than_five=list(filter(lambda x:x>5,lst)) # [6, 7, 8, 9, 10]
even_and_greater_than_five=list(filter(lambda x:x>5 and x%2==0,lst)) # [6, 8, 10]

people=[
	{'name':'Krish','age':32},
	{'name':'Jack','age':33},
	{'name':'John','age':25}
]

def age_greater_than_25(person):
	return person['age']>25
list(filter(age_greater_than_25,people)) # [{'name': 'Krish', 'age': 32}, {'name': 'Jack', 'age': 33}]
```

# Error handling
- Exceptions are events that disrupt the normal flow of a program. They occur when an error is encountered during program execution.
## Error Types
### Name Error
```python
try:
	a=b # NameError: name 'b' is not defined
except:
	print("The variable has not been assigned") # The variable has not been assigned
	
try:
	a=b
except NameError as ex:
	print(ex) # name 'b' is not defined
	
try:
	result=1/2
	a=b
except ZeroDivisionError as ex:
	print(ex)
	print("Please enter the denominator greater than 0")
except Exception as ex1:
	print(ex1) # name 'b' is not defined
	print('Main exception got caught here')
```
### Syntax Error
```python
@name="Krish" # SyntaxError: invalid syntax. Maybe you meant '==' or ':=' instead of '='?
```
### Value Error
```python
# invalid value
name="Krish"
int(name) # ValueError: invalid literal for int() with base 10: 'Krish'
```
### Type Error
```python
# invalid type
result="Hello" + 5 
# TypeError: can only concatenate str (not "int") to str

not file.closed()
TypeError: 'bool' object is not callable
```
### Key Error
```python
my_set=set([1,2,3,4,5,6])
my_set.remove(10) # KeyError: 10
```
### ZeroDivisionError
```python
# dividing by zero
try:
	result=1/0
except ZeroDivisionError as ex:
	print(ex) # division by zero
	print("Please enter the denominator greater than 0")
```
### FileNotFoundError
```python
# File not found
```
### Attribute Error
```python
class Car:
	pass
	
audi=Car()
audi.windows=4

tata=Car()
tata.doors=4
print(tata.windows) # AttributeError: 'Car' object has no attribute 'windows'
```

## file handling
```python
if 'file' in locals():
	print(True) # True

# -------------
try:
	file=open('example1.txt','r')
	content=file.read()
	a=b
	print(content)
except FileNotFoundError:
	print("The file does not exists")
except Exception as ex:
	print(ex)
finally:
	if 'file' in locals() or not file.closed():
		file.close()
		print('file close')
# name 'b' is not defined
# file close
```
## try, except, else, finally block
```python
try:
	num = int(input("Enter a number: "))
	result = 10 / num
except ValueError:
	print("That's not a valid number!")
except ZeroDivisionError:
	print("You can't divide by zero!")
except Exception as ex:
	print(ex)
else:
	print(f"The result is {result}")
finally:
	print("Execution complete.")
	
# input 0
# You can't divide by zero! 
# Execution complete.
```
## Custom Exception handling
```python
class Error(Exception):
	pass

class dobException(Error):
	pass
	
year = int(input("Enter the dob"))
age = 2025 - year

try:
	if age <= 30 and age >= 20:
		print("The age is valid")
	else:
		raise dobException
except dobException:
	print("the age is invalid")
```
# Libraries & Modules
# File handling
## Read file
```python
### Read a Whole File
with open('example.txt','r') as file: # example.txt in the same dir
	content=file.read()
	print(content)
# hello
# how are you?
	
# Read a file line by line
with open('example.txt','r') as file:
	for line in file:
		print(line.strip()) ## strip() removes the newline character
# hello
# how are you?

#Read a text file and count the number of lines, words, and characters.
# Counting lines, words, and characters in a text file
def count_text_file(file_path):
	with open(file_path, 'r') as file:
		lines = file.readlines()
		line_count = len(lines)
		word_count = sum(len(line.split()) for line in lines)
		char_count = sum(len(line) for line in lines)
	return line_count, word_count, char_count

file_path = 'example.txt'
lines, words, characters = count_text_file(file_path)
print(f'Lines: {lines}, Words: {words}, Characters: {characters}')

# Reading a binary file
with open('example.bin', 'rb') as file:
	content = file.read()
	print(content) # b'\x00\x01\x02\x03\x04'

```
## Write file
```python
## Writing a file(Overwriting)
with open('example.txt','w') as file:
	file.write('Hello World!\n')
	file.write('this is a new line.')
	
## Write a file(wwithout Overwriting)
with open('example.txt','a') as file:
	file.write("Append operation taking place!\n")
	
### Writing a list of lines to a file
lines=['First line \n','Second line \n','Third line\n']
with open('example.txt','a') as file:
	file.writelines(lines)
	
# Writing to a binary file
data = b'\x00\x01\x02\x03\x04'

with open('example.bin', 'wb') as file:
	file.write(data)
```

## Read and Write
```python
# Read the content froma source text fiile and write to a destination text file
# Copying a text file
with open('example.txt', 'r') as source_file:
	content = source_file.read()
	
with open('destination.txt', 'w') as destination_file:
	destination_file.write(content)
	
# The w+ mode in Python is used to open a file for both reading and writing. If the file does not exist, it will be created. If the file exists, its content is truncated (i.e., the file is overwritten).
### Writing and then reading a file
with open('example.txt','w+') as file:
	file.write("Hello world\n")
	file.write("This is a new line \n")
	
	## Move the file cursor to the beginning
	file.seek(0)
	
	## Read the content of the file
	content=file.read()
	print(content)
```
## File Path
```python
#### Using the os module
import os

cwd=os.getcwd()
print(f"Current working directory is {cwd}") # Current working directory is e:\UDemy Final\python\6-File Handling

## create a new directory
new_directory="package"
os.mkdir(new_directory)
print(f"Directory '{new_directory}' created") # Directory 'package' created

## Listing Files And Directories
items=os.listdir('.')
print(items) # ['6.1-fileoperation.ipynb', '6.2-filepath.ipynb', 'destination.txt', 'example.bin', 'example.txt', 'package']

### Joining Paths
dir_name="folder"
file_name="file.txt"
full_path=os.path.join(dir_name,file_name)
full_path2=os.path.join(os.getcwd(),dir_name,file_name)
print(full_path) # folder\file.txt
print(full_path2) # e:\UDemy Final\python\6-File Handling\folder\file.txt

path='example1.txt'

if os.path.exists(path):
	print(f"The path '{path}' exists") 
else:
	print(f"The path '{path}' does not exists") # The path 'example1.txt' does not exists
	
	
#Checking if a Path is a File or Directory
import os

path = 'example.txt'

if os.path.isfile(path):
	print(f"The path '{path}' is a file.") # The path 'example.txt' is a file.
elif os.path.isdir(path):
	print(f"The path '{path}' is a directory.")
else:
	print(f"The path '{path}' is neither a file nor a directory.")
	
	
## Getting the absolute path
relative_path='example.txt'
absolute_path=os.path.abspath(relative_path)
print(absolute_path) # e:\UDemy Final\python\6-File Handling\example.txt

```
# Language Specific
## Iterators
Iterators are advanced Python concepts that allow for efficient looping and memory management. Iterators provide a way to access elements of a collection sequentially without exposing the underlying structure.
```python
my_list=[1,2,3,4,5,6]
iterator=iter(my_list)
print(type(iterator)) # <class 'list_iterator'>
iterator # <list_iterator at 0x27a325efb20>

## Iterate through all the element
next(iterator) # 1

try:
	print(next(iterator)) # 1
except StopIteration:
	print("There are no elements in the iterator")
	
# String iterator
my_string = "Hello"
string_iterator = iter(my_string)

print(next(string_iterator)) # Output: H
print(next(string_iterator)) # Output: e
```
## Generators
Generators are a simpler way to create iterators. They use the yield keyword to produce a series of values lazily, which means they generate values on the fly and do not store them in memory. Iterators provide a way to access elements sequentially, while generators allow you to generate items on the fly, making them particularly useful for handling large datasets and infinite sequences.
```python
def square(n):
	for i in range(3):
		yield i**2
		
square(3) # <generator object square at 0x79e45048e260>

for i in square(4):
	print(i) # 0 1 4
	
a=square(3)
a # <generator object square at 0x79e45048e400>
next(a) # 0

def my_generator():
	yield 1
	yield 2
	yield 3
	
gen=my_generator()
next(gen) # 1

for val in gen:
	print(val) # 2 3
	
	
# Reading Large files
def read_large_file(file_path):
	with open(file_path,'r') as file:
		for line in file:
			yield line
			
file_path='large_file.txt'
for line in read_large_file(file_path):
	print(line.strip())
```
## Decorators
Decorators are a powerful and flexible feature in Python that allows you to modify the behavior of a function or class method. They are commonly used to add functionality to functions or methods without modifying their actual code. They provide a clean and readable way to add functionality such as logging, timing, access control, and more without changing the original code.
### function copy
```python
## function copy
def welcome():
	return "Welcome to python"
	
welcome()
wel=welcome
print(wel()) # Welcome to python
del welcome
print(wel()) # Welcome to python
```
### closure function
```python
def main_welcome(msg):
	def sub_welcome_method():
		print("first line")
		print(msg)
		print("third line")
	return sub_welcome_method()
	
main_welcome("Welcome everyone")
# first line
# Welcome Everyone
# third line

def main_welcome(func):
	def sub_welcome_method():
		print("first line")
		func("msg")
		print("third line")
	return sub_welcome_method()
	
main_welcome(print)
# first line
# msg
# third line

def main_welcome(func,lst):
	def sub_welcome_method():
		print("first line")
		print(func(lst))
		print("third line")
	return sub_welcome_method()
	
main_welcome(len,[1,2,3,4,5])
# first line
# 5
# third line
```
### decorator
```python
def main_welcome(func):
	def sub_welcome_method():
		print("first line")
		func()
		print("third line")
	return sub_welcome_method()
	
def coure_introduction():
	print("second line")

main_welcome(coure_introduction)
# first line
# second line
# third line

@main_welcome
def course_introduction():
	print("second line")

course_introduction()
# first line
# second line
# third line

## Decorators WWith arguments
def repeat(n):
	def decorator(func):
		def wrapper(*args, **kwargs):
			for _ in range(n):
				func(*args, **kwargs)
		return wrapper
	return decorator
	
@repeat(3)
def say_hello():
	print("Hello")

say_hello()
# Hello
# Hello
# Hello
```
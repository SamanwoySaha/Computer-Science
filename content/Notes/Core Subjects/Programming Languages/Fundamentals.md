---
title: Fundamentals
draft: false
tags: 
date: 10-Aug-2025
---
# Basic Syntax and Structure
## Syntax

Syntax refers to the set of rules that defines the combinations of symbols that are considered to be correctly structured programs in a language. In simpler terms, syntax is about the correct arrangement of words and symbols in a code.
## Semantics

Semantics refers to the meaning or the interpretation of the symbols, characters, and commands in a language. It is about what the code is supposed to do when it runs.
## Variables
- used to store data that can be referenced and manipulated in a program
- Variable names should be descriptive
- must start with a letter or an '_' and contains letter,numbers and underscores
- case sensitive
```python
#valid variable names
first_name="KRish"
last_name="Naik"

# Invalid variable names
#2age=30
#first-name="Krish"
##@name="Krish"
```
## Data Type
- determine the type of operations that can be performed on the data, the values that the data can take, and the amount of memory needed to store the data.
- Basic Data Types
	- Integers
	- Float
	- String
	- Boolean
```python
age=25 #int
height=6.1 #float
name="KRish" #str
is_student=True #bool
a=10; b=10
type(a==b) # bool
```
### String
```python
### Counting Unique words in text
text="In this tutorial we are discussing about sets"
words=text.split()

## convert list of words to set to get unique words
unique_words=set(words)
print(unique_words) # {'tutorial', 'we', 'discussing', 'this', 'In', 'about', 'sets', 'are'}
print(len(unique_words)) # 8
```
### Dynamic Typing
- type of a variable to change as the program executes
```python
var=10 #int
print(var,type(var)) # 10 <class 'int'>

var="Hello"
print(var,type(var)) # Hello <class 'str'>

var=3.14
print(var,type(var)) # 3.14 <class 'float'>
```
### Type Conversion
```python
age=25
print(type(age)) # <class 'int'>

# Type conversion
age_str=str(age)
print(age_str) # 25
print(type(age_str)) # <class 'str'>
print(type(int(age))) # <class 'int'>
```
# Operators
## Arithmetic operators 

```js
/*
There are the arithmetic operator in JavaScript 
    +   Addition
    -	Subtraction
    *	Multiplication
    /	Division
    %	Modulus (division remainder)
    **  Exponentiation
    ++	Increment	
    --	Decrement
    **  power
*/

let x = 10;
let y = 3;

console.log(x + y);
console.log(x - y);
console.log(x * y);
console.log(x / y);
console.log(x % y);
console.log(x ** y); // x to the power of y


// ++ Incremete operator behaves differently depending on where we put the operator.
console.log(++x); // If we put increment before x, first the value of x first will be incremented by 1, and then we see x it in the console.
console.log(x++); // If we put increment after x, first we see it in the console, and them the value of x will be incremented by 1.
console.log(x);

// -- Decrement operator behaves just like the Increment, but subtract 1.
console.log(--x);
console.log(x--);
console.log(x);
```
### Operator precedence

```js
/*
Operators have precedence
Just like in math the expression between the parentheses "()" are evaluated first.
*/

let x = 2 + 4 * 3 // Here the * operator has higher precedence so 4 * 3 is calculates first and then add 2 so the result is 14
console.log(x)

let y = (2 + 3) * 4 // Here because we use parentheses in (2 + 4) this is calculates first and then we add 3 so the result is 20
console.log(y)
```
## Relational / Comparison operators 

```js
/*
An expression with a comparison operator will return a boolean value
These are the comparison operators
    ==	equal to	
    ===	equal value and equal type
    !=	not equal
    !==	not equal value or not equal type	
    >	greater than
    <	less than	
    >=	greater than or equal to
    <=	less than or equal to
*/

let x = 5;

console.log(x == '5');
console.log(x === 5);
console.log(x != '5');
console.log(x !== 5);
console.log(x > 5);
console.log(x < 5);
console.log(x >= 5);
console.log(x <= 5);

// 05- Equality Operators

/*
As we seen in the last lectures we have different equality operators
    ==	equal to	
    ===	equal value and equal type
    !=	not equal
    !==	not equal value or not equal type	
*/

// Strict Equality operator (checks for Type + Value) 
// Ina strict equality operator both values have to be of the same type and mus have the same value
console.log(1 === 1) // This returns true because we are comparing the same type to the same value
console.log('1' === 1) // This returns false because we are comparing different types, a string to number.


// Lose Equality operator (checks for Value)
console.log(1 == 1) // Here we get true
console.log('1' == 1) // Here we also get true. Because this operator will look at the first part and see a string, then it will convert the second part to a string, and if they became the same value will return true.
console.log(true == 1) // Here we get true as well. Because when we convert 1 to boolean it will be true 
console.log(false === 1) // Here we ge false.
console.log(false == 0) // Here we also get true because 0 is a false value.
```
## Logical operators 

```js
/*
Logical operators are used to determine the logic between variables or values. To make decisions on multiple conditions.
These are the logical operators
    &&	(and operator) With the and operator both conditions or operator have to be true.
    ||	(or operator)  With the or operator only one of the conditions has to be true.
    !	(not operator) The not operator converts true to false and vice-versa.
x = 6 and y = 3
(x < 10 && y > 1) is true
(x === 5 || y === 5) is false
!(x === y) is true
*/

// Lets say we want to determine if some one is eligible for a loan, based on is income and credit score.

let hiIncome = false
let goodCreditScore = true

let eligibleForLoan = hiIncome && goodCredit // With and operator "&&" applicant has to have high income and good credit score to be eligible for loan.
console.log(eligibleForLoan)

eligibleForLoan = hiIncome || goodCredit // With or operator "||" applicant has to have high income or good credit score to be eligible for loan. If one of them is true elidible for loan will be true.
console.log(eligibleForLoan)

let applicationRefused = !eligibleForLoan
console.log(applicationRefused)
// With not operator "!" it will convert true to false and false to true.
//So if the applicant is not eligible for loan, meaning "eligibleForLoan = false", is application will be refused meaning "applicationRefused = !eligibleForLoan" will return true.

// 08- Logical Operators with Non-booleans

/*
We can use the logical operators with non boolean values
    &&
    ||
    !

The result of the logical expression it is not necessarily a boolean value true or false.
That depends on the value of the operands we have.
The logical operations looks at each operant, and if the operand is not a boolean true or false, it will try to interpret it as Truthy or Falsy.

Falsy values (False)
    false
    undefined
    null
    0
    '' (empty string)
    NaN (Not a Number)

If we use any of this values in a logical operation, they will be treated as falsy. Which is kind a like a boolean False, but is not exactly the same.
Any other value that is not Falsy is Truthy.

*/

console.log(false || true) // This will return true
console.log(false || 'Miguel') // This will return true because a non empty string is a Truthy value.
console.log(false || -1) // This will return true because any number different of 0 is a Truthy value.
console.log(false || 1 || 2) // This returns 1 because is the first Truthy operand.

// When using the '||' or operator the evaluation starts in the first operand, and stops in the first Truthy value it finds, if there are any.
// This is called short-circuiting

// A real world example to use this could be for default values.
// For example if a user picks a color we that color, if we does not pick a color we use the default value.

let userColor = 'red'
let defaultColor = 'blue'
console.log(userColor || defaultColor) // This basically means that if we have a value for the user color we use that, if we don't we use the default color.

userColor = undefined
console.log(userColor || defaultColor) // Here the user did not pick a color, the variable user is set to undefined, so we will use the default color.
```
## Bitwise operators 

```js
/*
Bit operators work on 32 bits numbers. Any numeric operand in the operation is converted into a 32 bit number. The result is converted back to a JavaScript number.
    &	AND
    |	OR
    ~	NOT
    ^	XOR
    <<	Left shift
    >>	Right shift

We humans use de decimal system to represent numbers 0..9, but in computers this numbers are stored in the binary format, which is a combination of 0 and 1
1 = 00000001
2 = 00000010
3 = 00000011
In binary each number is a bit.
Bitwise operator as similar to logical operator but they or on each bit of the number.
*/

console.log(1 | 2)
/*
Using the bitwise "|"  operator it will compare each bit (0 and 1) in its equivalent position, and where he finds 1 the result will be 1 otherwise it will be 0.
     1 = 00000001
     2 = 00000010
result = 00000011 ---> 3 represents 3 in decimal number
*/

console.log(1 & 2)
/*
Using the bitwise "&" operator it will compare each bit (0 and 1), and it will return 1 if both operands have 1 in the same position, otherwise it will return 0.
     1 = 00000001
     2 = 00000010
result = 00000000 ---> 0 represents 0 in decimal number
*/

/*
For a real world example
Lets say we want to implement an access controle system.
So the user can have this permissions:
    Read
    Write
    Execute
We can use one byte of information (the same as 8 bits) to determine the kind of permission a user has.
For each permission we assign one bit.
    Read                       ---> 00000100 ---> 4 in decimal
    Write                      ---> 00000010 ---> 2 in decimal
    Execute                    ---> 00000001 ---> 1 in decimal

    Read                       ---> 00000100 ---> 4 in decimal
    Read and Write             ---> 00000110 ---> 6 in decimal
    Read and Write and Execute ---> 00000111 ---> 7 in decimal
We are representing the permissions in binary numbers. For
*/

const readPermission = 4; // We convert the binary number 00000100 to decimal, which is 4.
const writePermission = 2; // We convert the binary number 00000010 to decimal, which is 2.
const executePermission = 1; // We convert the binary number 0000001 to decimal, which is 1.

let myPermission = 0; // We declare a variable and initially we do not have any permissions 0 decimal equal to 00000000 binary

myPermission = myPermission | readPermission; // With the bitwise "|" operator we are assign the read permission to the user 
console.log(myPermission)

myPermission = myPermission | writePermission; // And here we add the write permission.
console.log(myPermission);

let message = myPermission & executePermission ? 'yes' : 'no'; // We we check if the user has the Execute permission with the "&" operator.

// With the bitwise "|" we can add permission, and with the bitwise "&" operator we can che to see if the user has permissions.
```
## Assignment operators 

```js
/*
Theses are the assignment operator: 
    =
    +=
    -=
    *=
    /=	
    %=
*/

let x = 10; // Assigning 10 to x

console.log(x += 5); // This is the same as x = x + 5
console.log(x -= 5); // This is the same as x = x - 5
console.log(x *= 5); // This is the same as x = x * 5
console.log(x /= 5); // This is the same as x = x / 5
console.log(x %= 5); // This is the same as x = x % 5
```
# Control Structures 
## Conditional Statements
```python
age=17

if age<13:
	if age <= 1:
		print("You are an infant")
	else:
		print("You are a child")
elif age<18:
	print("You are a teenager") # You are a teenager
else:
	print("You are an adult")
```
## Loop
```python
# while loop
count=0

while count<5:
	print(count) # 0 1 2 3 4
	count=count+1

# for loop
for i in range(3):
	for j in range(2):
		print(f"i:{i} and j:{j}")
# i:0 and j:0 
# i:0 and j:1 
# i:1 and j:0 
# i:1 and j:1 
# i:2 and j:0 
# i:2 and j:1
```
### Loop Control Statements
#### Break
```python
# exits the loop permaturely
for i in range(10):
	if i==5:
		break
	print(i) 
# 0 1 2 3 4
```
#### Continue
```python
# skips the current iteration and continues with the next.
for i in range(10):
	if i%2==0:
		continue
	print(i)
# 1 3 5 7 9
```
# Data Structures
# Functions 
- block of code that performs specific task. 
```python
def add(a,b):
	return a+b

result=add(2,4)
print(result) # 6

# default parameter
def greet(name="Guest"):
	print(f"Hello {name} Welcome To the paradise")
greet("Krish") # Hello Krish Welcome To the paradise
greet() # Hello Guest Welcome To the paradise

```

# Error handling
- Exceptions and error handling mechanisms (try, catch, finally)
- Throwing errors
- Debugging techniques
# Memory Management
# Libraries & Modules
# File handling
- Reading from and writing to files
- File streams and buffers
- File formats (e.g., text, binary, JSON)
# Data Serialization
- Parsing and serializing data (e.g., JSON, XML)
- Saving and retrieving structured data
# Concurrency and Parallelism
- Threads and processes
- Synchronization mechanisms (locks, semaphores)
- Asynchronous programming (e.g., async/await)
# Compilation and Interpretation
- Understanding how code runs (compiled vs. interpreted languages)
- Linking, runtime, and execution phases
# Testing and Debugging
- Profiling tools to analyze performance
- Memory leak detection
- Race condition debugging
- Writing test cases
- Unit testing, integration testing
- Debugging techniques and tools
# Networking
- Making HTTP requests
- Basic socket programming
- API integration (e.g., RESTful APIs)
# Development Tools
# Build and Deployment
- Compilation and linking
- Continuous Integration/Continuous Deployment (CI/CD)
- Dependency management
# Security
- Authentication and authorization
- Encryption and hashing
- Input validation and sanitization
# Software Design Principles
- Modularity and code reuse
- Design patterns (e.g., Singleton, Factory, Observer)
- DRY (Don't Repeat Yourself)
- SOLID principles
# Programming Paradigms
- Procedural
- Object-oriented
- Functional
- Declarative
- Event-driven
# Advanced Topics
- Generics/templates
- Metaprogramming and reflection
- Domain-specific languages (DSLs)
- Compilers and interpreters
# Advanced Type Systems
- Type inference
- Union and intersection types
- Algebraic data types
- Subtyping and variance
# Meta-programming
- Reflection and introspection
- Code generation
- Annotation processing
# Language Specific 
- Macros (e.g., Rust, C)
- Coroutines (e.g., Python, Kotlin)
- Extension methods (e.g., C#, Kotlin)
# Low level programming
- Assembly language basics
- Memory alignment and paging
- Direct hardware interaction (e.g., via syscall)
# Cross platform development
- Writing portable code
- Endianness considerations
- Platform-specific optimizations
# Interfacing with other language
- Foreign Function Interface (FFI)
- Language bindings (e.g., Python <-> C)
# Domain specific 
- Game development (game loops, physics engines)
- Data science and machine learning (numerical computing)
- Web development (REST, GraphQL, WebSocket)
# Tooling and ecosystem
- Package managers (e.g., npm, pip, Cargo)
- IDE and editor setup
- Linters and formatters




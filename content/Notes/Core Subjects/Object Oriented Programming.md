---
title: Object Oriented Programming
draft: false
tags:
date: 10-Aug-2025
---
# References
1. [Object Oriented Programming with Python - Full Course for Beginners - YouTube](https://www.youtube.com/watch?v=Ej_02ICOIgs)
# Introduction
Object-Oriented Programming (OOP) is a programming paradigm that uses "objects" to design applications and computer programs. OOP allows for modeling real-world scenarios using classes and objects.

```python
item1 = 'Phone'
item1_price = 100
item1_quantity = 5
item1_price_total = item1_price * item1_quantity

print(type(item1)) # <class 'str'> instance of str class
print(type(item1_price)) # <class 'int'>
print(type(item1_quantity)) # <class 'int'>
print(type(item1_price_total)) # <class 'int'>
```
## class and object
A class is a blue print for creating objects. Objects are instances of class
```python
class Dog:
	# constructor
	def __init__(self,name,age):
		self.name=name # attributes
		self.age=age 
		
	def bark(self): # methods
		print(f"{self.name} says woof")

## create objects
dog1=Dog("Buddy",3)
print(dog1.name) # Buddy
print(dog1.age) # 3
dog1.bark() # Buddy says woof

### Modeling a Bank Account
## Define a class for bank account
class BankAccount:
	def __init__(self,owner,balance=0):
		self.owner=owner
		self.balance=balance
	  
	def deposit(self,amount):
		self.balance+=amount
		print(f"{amount} is deposited. New balance is {self.balance}")
	
	def withdraw(self,amount):
		if amount>self.balance:
			print("Insufficient funds!")
		else:
			self.balance-=amount
			print(f"{amount} is withdrawn. New Balance is {self.balance}")
	
	def get_balance(self):
	return self.balance

## create an account
account=BankAccount("Krish",5000)
print(account.balance) # 5000
account.deposit(100)
account.withdraw(300)
print(account.balance) # 4800


## another example
class Item:
	def __init__(self, name):
		print(f"I am created: {name}")
	
	def calculate_total_price(self, x, y): # method
		return x * y

item1 = Item("Phone") # I am created: Phone
item1.name = 'Phone' # attributes
item1.price = 100
item1.quantity = 5
item1.calculate_total_price(item1.price, item1.quantity) # 500

item2 = Item() # I am created: Laptop
item2.name = 'Laptop' # attributes
item2.price = 1000
item2.quantity = 3
item2.calculate_total_price(item2.price, item2.quantity) # 3000

print(type(item1)) # # <class '__main__.Item'>
print(item1) # <__main__.Item object at 0x0000015A0B79FF20>
dir(item1)
# ['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getstate__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'name', 'price', 'quantity']
print(type(item1.name)) # <class 'str'>
print(type(item1.price)) # <class 'int'>
print(type(item1.quantity)) # <class 'int'>


class Item:
	pay_rate = 0.8 # class attribute
	all = []
	def __init__(self, name: str, price: float, quantity = 0):
		# validation
		assert price >= 0, f"Price {price} is not greater than or equal to zero!"
		assert quantity >= 0 f"Quantity {quantity} is not greater than or equal to zero!"
	
		# assign to self object
		self.name = name
		self.price = price
		self.quantity = quantity
		
		# actions to execute
		Item.all.append(self)
	
	def calculate_total_price(self): # method
		return self.price * self.quantity
		
	def apply_discount(self):
		# self.price = self.price * Item.pay_rate
		self.price = self.price * self.pay_rate
		
	def __repr__(self):
		return f"Item('{self.name}', {self})"

item1 = Item("Phone", 100, 5)
item2 = Item("Laptop", 1000, 3)
item3 = Item("Cable", 10, 5)
item4 = Item("Mouse", 50, 5)
item5 = Item("Keyboard", 75, 5)

print(Item.all) 
# without repr
# [<__main__.Item object at 0x7ebea3537380>, <__main__.Item object at 0x7ebea2d71310>, <__main__.Item object at 0x7ebea2d71450>, <__main__.Item object at 0x7ebea35a6190>, <__main__.Item object at 0x7ebea35a5e00>]

# with repr
# [Item('Phone', 100, 5), Item('Laptop', 1000, 3), Item('Cable', 10, 5), Item('Mouse', 50, 5), Item('Keyboard', 75, 5)]

for instance in Item.all:
	print(instance.name) 

item2.has_numpad = False # additional attribute

item3  = Item("Charger" 50) # optional argument

print(item1.name) # Phone
print(item2.name) # Laptop
print(item.calculate_total_price()) # 500

print(Item.pay_rate) # 0.8
print(item1.pay_rate) # 0.8

print(Item.__dict__) # all the class level attributes
print(item1.__dict__) # all the instance level attributes

item1.apply_discount()
print(item1.price) # 80

item2.pay_rate = 0.7 
item2.apply_discount() 
# self.price = self.price * Item.pay_rate
print(item2.price) # 800 still pay_rate = 0.8 from cllass level

# self.price = self.price * self.pay_rate
print(item2.price) # 700 still pay_rate = 0.7 from instance



```
## Class vs Static Methods

```python
import csv

class Item:
	def __init__(self, name, price, quantity):
		self.name = name
		self.price = price
		self.quantity = quantity
		
	@classmethod
	def instantiated_from_csv(cls):
		with open('items.csv', 'r') as file:
			reader = csv.DictReader(file)
			items = list(reader)
			
		for item in items:
			Item(
				name=item.get('name'),
				price=float(item.get('price')),
				quantity=int(item.get('quantity')),
			)
			
	@staticmethod
	def is_integer(num):
		# count out the floats that are point zero
		# For i.e: 5.0, 10.0
		if isinstance(num, float):
			# count out the floats that are point zero
			return num.is_integer()
		elif isinstance(num, int):
			return True
		else:
			return False

Item.instantiate_from_csv()
print(Item.all)

# When to use class methods and when to use static methods ?

class Item:
    @staticmethod
    def is_integer():
        '''
        This should do something that has a relationship
        with the class, but not something that must be unique
        per instance!
        '''
    @classmethod
    def instantiate_from_something(cls):
        '''
        This should also do something that has a relationship
        with the class, but usually, those are used to
        manipulate different structures of data to instantiate
        objects, like we have done with CSV.
        '''

# THE ONLY DIFFERENCE BETWEEN THOSE:
# Static methods are not passing the object reference as the first argument in the background!


# NOTE: However, those could be also called from instances.

item1 = Item()
item1.is_integer()
item1.instantiate_from_something()
```
## Inheritance
allows a class to inherit attributes and methods from another class.
### Single Inheritance
```python
## Parent class
class Car:
	def __init__(self,windows,doors,enginetype):
		self.windows=windows
		self.doors=doors
		self.enginetype=enginetype
	
	def drive(self):
		print(f"The person will drive the {self.enginetype} car ")
		
car1=Car(4,5,"petrol")
car1.drive() # The person will drive the petrol car

class Tesla(Car):
	def __init__(self,windows,doors,enginetype,is_selfdriving):
		super().__init__(windows,doors,enginetype)
		self.is_selfdriving=is_selfdriving
	
	def selfdriving(self):
		print(f"Tesla supports self driving : {self.is_selfdriving}")
		
tesla1=Tesla(4,5,"electric",True)
tesla1.selfdriving() # Tesla supports self driving : True
tesla1.drive() # The person will drive the electric car





```

```python title="item.py"
import csv

class Item:
    pay_rate = 0.8 # The pay rate after 20% discount
    all = []
    def __init__(self, name: str, price: float, quantity=0):
        # Run validations to the received arguments
        assert price >= 0, f"Price {price} is not greater than or equal to zero!"
        assert quantity >= 0, f"Quantity {quantity} is not greater or equal to zero!"

        # Assign to self object
        self.name = name
        self.price = price
        self.quantity = quantity

        # Actions to execute
        Item.all.append(self)

    def calculate_total_price(self):
        return self.price * self.quantity

    def apply_discount(self):
        self.price = self.price * self.pay_rate

    @classmethod
    def instantiate_from_csv(cls):
        with open('items.csv', 'r') as f:
            reader = csv.DictReader(f)
            items = list(reader)

        for item in items:
            Item(
                name=item.get('name'),
                price=float(item.get('price')),
                quantity=int(item.get('quantity')),
            )

    @staticmethod
    def is_integer(num):
        # We will count out the floats that are point zero
        # For i.e: 5.0, 10.0
        if isinstance(num, float):
            # Count out the floats that are point zero
            return num.is_integer()
        elif isinstance(num, int):
            return True
        else:
            return False

    def __repr__(self):
        return f"{self.__class__.__name__}('{self.name}', {self.price}, {self.quantity})"
```

```python title="phone.py"
class Phone(Item):
    def __init__(self, name: str, price: float, quantity=0, broken_phones=0):
        # Call to super function to have access to all attributes / methods
        super().__init__(
            name, price, quantity
        )

        # Run validations to the received arguments
        assert broken_phones >= 0, f"Broken Phones {broken_phones} is not greater or equal to zero!"

        # Assign to self object
        self.broken_phones = broken_phones

phone1 = Phone("jscPhonev10", 500, 5, 1)

print(Item.all)
```

```python title="app.py"
from item import Item
from phone import Phone

Item.instantiate_from_csv()

print(Item.all)
```
### Multiple Inheritance
```python
## When a class inherits from more than one base class.

## Base class 1
class Animal:
	def __init__(self,name):
		self.name=name
	
	def speak(self):
		print("Subclass must implement this method")

## BAse class 2
class Pet:
	def __init__(self, owner):
		self.owner = owner

##Derived class
class Dog(Animal,Pet):
	def __init__(self,name,owner):
		Animal.__init__(self,name)
		Pet.__init__(self,owner)
	
	def speak(self):
		return f"{self.name} say woof"

## Create an object
dog=Dog("Buddy","Krish")
print(dog.speak()) # Buddy say woof
print(f"Owner:{dog.owner}") # Owner:Krish
```
## Polymorphism
- allows objects of different classes to be treated as objects of a common superclass
- provides a way to perform a single action in different forms
- typically achieved through method overriding and interfaces
### Method Overriding
allows a child class to provide a specific implementation of a method that is already defined in its parent class.
```python
## Base Class
class Animal:
	def speak(self):
		return "Sound of the animal"

## Derived Class 1
class Dog(Animal):
	def speak(self):
		return "Woof!"

## Derived class
class Cat(Animal):
	def speak(self):
		return "Meow!"

## Function that demonstrates polymorphism
def animal_speak(animal):
	print(animal.speak())
	
dog=Dog()
cat=Cat()
print(dog.speak()) # Woof!
print(cat.speak()) # Meow!
animal_speak(dog) # Woof!


# Polymorphism with functions and methods
# base class
class Shape:
	def area(self):
		return "The area of the figure"
		
# Derived class 1
class Rectangle(Shape):
	def __init__(self,width,height):
		self.width=width
		self.height=height
	
	def area(self):
		return self.width * self.height

##DErived class 2  
class Circle(Shape):
	def __init__(self,radius):
		self.radius=radius
	
	def area(self):
		return 3.14*self.radius *self.radius

## Fucntion that demonstrates polymorphism
def print_area(shape):
	print(f"the area is {shape.area()}")

rectangle=Rectangle(4,5)
circle=Circle(3)

print_area(rectangle) # the area is 20
print_area(circle) # the area is 28.259999999999998
```
### Abstract Base Class
Abstract Base Classes (ABCs) are used to define common methods for a group of related objects. They can enforce that derived classes implement particular methods, promoting consistency across different implementations.
```python
from abc import ABC,abstractmethod

## Define an abstract class
class Vehicle(ABC):
	@abstractmethod
	def start_engine(self):
		pass

## Derived class 1
class Car(Vehicle):
	def start_engine(self):
		return "Car enginer started"

## Derived class 2
class Motorcycle(Vehicle):
	def start_engine(self):
		return "Motorcycle enginer started"

# Function that demonstrates polymorphism
def start_vehicle(vehicle):
	print(vehicle.start_engine())

## create objects of cAr and Motorcycle
car = Car()
motorcycle = Motorcycle()

start_vehicle(car) # Car enginer started
```
## Encapsulation
Encapsulation involves bundling data and methods that operate on the data within a single unit. Encapsulation is the concept of wrapping data (variables) and methods (functions) together as a single unit. It restricts direct access to some of the object's components, which is a means of preventing accidental interference and misuse of the data.
### Access modifier
```python
class Person:
	def __init__(self, name, age, gender):
		self.name = name # public (Fully accessible from anywhere.)
		self.__age = age # private (prevent direct access.)
		self._gender = gender # protected (Access is discouraged, but not prevented.)
	
	def get_name(person):
		return person.name
	
	def get_age(person):
		return person.__age
		
	def get_gender(person):
		return person._gender
	
	person=Person("Krish",34, "Male")
	get_name(person) # Krish
	get_age(person) # AttributeError: 'Person' object has no attribute '__age'
	dir(person)
	['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getstate__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'name']
	
class Employee(Person):
	def __init__(self,name,age,gender):
		super().__init__(name,age,gender)
		
employee=Employee("Krish",34,"Male")
print(employee._gender) # Krish
```
### Getter and Setter

```python
class Person:
	def __init__(self,name,age):
		self.__name=name ## Private access modifier or variable
		self.__age=age ## Private variable
	
	## getter method for name
	def get_name(self):
		return self.__name
	
	## setter method for name
	def set_name(self,name):
		self.__name=name
	
	# Getter method for age
	def get_age(self):
		return self.__age
	
	# Setter method for age
	def set_age(self, age):
		if age > 0:
			self.__age = age
		else:
			print("Age cannot be negative.")

person=Person("Krish",34)

## Access and modify private variables using getter and setter
print(person.get_name()) # Krish
print(person.get_age()) # 34
person.set_age(35)
print(person.get_age()) # 35
person.set_age(-5) # Age cannot be negative.
```
## Abstraction
concept of hiding the complex implementation details and showing only the necessary features of an object
```python
from abc import ABC,abstractmethod

## Abstract base cclass
class Vehicle(ABC):
	def drive(self):
		print("The vehicle is used for driving")
	
	@abstractmethod
	def start_engine(self):
		pass

class Car(Vehicle):
	def start_engine(self):
		print("Car enginer started")
	
	def operate_vehicle(vehicle):
		vehicle.start_engine()
		vehicle.drive()

car=Car()
operate_vehicle(car)
# Car enginer started
# The vehicle is used for driving
```
## Magic Methods
Magic methods in Python, also known as dunder methods (double underscore methods), are special methods that start and end with double underscores. These methods enable you to define the behavior of objects for built-in operations, such as arithmetic operations, comparisons, and more.Some common magic methods include:
```python
__init__: Initializes a new instance of a class.
__str__: Returns a string representation of an object.
__repr__: Returns an official string representation of an object.
__len__: Returns the length of an object.
__getitem__: Gets an item from a container.
__setitem__: Sets an item in a container.

class Car:
	pass

car = Car()
print(car) # <__main__.Car object at 0x0000029E5D059940>

class Person:
	def __init__(self, name, age):
		self.name=name
		self.age=age
		
	def __str__(self):
		return f"{self.name},{self.age} years old"
	
	def __repr__(self):
		return f"Person(name={self.name},age={self.age})"

person=Person("KRish",34)
print(person) # KRish,34 years old
print(repr(person)) # Person(name=KRish,age=34)
dir(person) # ['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getstate__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'name', 'age']


```


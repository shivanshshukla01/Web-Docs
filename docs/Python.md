---
hide:
  - navigation
---
### Strings
```python
string = "Pluto is a planel!"

string.startswith("substring")
string.endswith("substring")

string.split() # list of words divided at spaces by default 
temp = "1956-454-841"
temp.split('-') # split from the -

string.join() # the reverse of the above
`/`.join([day, month, yer]) # 06/11/2025

pluto_mass = 1.303 * 10**22
earth_mass = 5.9722 * 10**24
population = 52910390
#         2 decimal points   3 decimal points, format as percent     separate with commas
"{} weighs about {:.2} kilograms ({:.3%} of Earth's mass). It is home to {:,} Plutonians.".format(
    planet, pluto_mass, pluto_mass / earth_mass, population,
)
```
- To learn more about `{:.2}`, `{:.3%}`, etc, Go to [Python Format Specification Mini-language Official Docs](https://docs.python.org/3/library/string.html#formatspec) or [pyformat.info](https://pyformat.info/)
### Functions
```python
def function_name(parameters):
	# code_here
	return value1, value2 # if you want to have some thing from the function as well to carry forward
	
x, y = function_name(arguments) # value1 will be assigned to x and value2 to y
# arguments and parameters are almost some, the difference is there place of declaration

# DEFAULT VALUES
def func1(a = 12):
	# some processing
	return result

word = "something"
word.find("e") # numeral, return the index of first occurance,
# if no occurance, return -1

"e" in word # boolean, return True or False
```

### List and Tuple
```python
list_data = ["content", "hello", 1.2, -1]

len(list_data)              # 4
sum(list_1)                 # adds all the elements of the list together
max(list_1)                 # returns the highest value in the list
min(list_1)
sorted(list_1)              # iterable as argument and then sort the list
# it creates a new list and do not interfere the data in original list
new_list = (list_1, reverse=True) # change the order

list_data.append("some_data")    # add the data at the end of the list
list_data.insert(index, "data2") # add the data at the specified
list_data.pop(index)             # deletes the item at the index
# also return the item that it deleted, no arguments - delete the last item
list_data.index("data") # return the index at which "data" is stored

for x in list_1:
	# in is used to easily check whether some element is the collection data type or not	


# TUPLES
tuple_data = (val1, val1, val2, val2, val2, val3, val4)

tuple_data.count(val1)            # 2
# ALL THE METHODS OF LIST CAN BE USED WITH TUPLES AS WELL AS LONG AS THEY ARE NOT BEING USED FOR MODIFICATIONS

sample_tuple = (some1, some2, some3)
data1, data2, data3 = sample_tuple # the values of tuple will be assigned to variables in the sequence of occurence BUT NUMBER OF VARIABLE SHOULD MATCH THE NUMBER OF ELEMENTS IN THE TUPLE

sample_tuple = (v1, v2, v3, v4, v5, v6, v7, v8, v9, v10, v11, v12, v13, v14) # unknown number of elements

first, second, *remaining = sample_tuple
# first will be assigned - v1
# second will be assigned - v2
# remaining will be assigned - a LIST of all the remaining items

new_list = [x for x in range(1, 51)]
variable = [expression for item in iterable if condition]
# expression is the operation that will be run on each item
# if no transformation needed, expression can be just items
# only operate the experssion on item if condition is True
new_list = [x*2 for x in range(1, 51)]
```

### Sets
- A datatype perfect for storing unique data.
- Unordered collection made with `{ }`. It means they do not support indexing or slicing.
- It cannot have duplicate data, even if there is, there will be no error but further occurrence will be ignored.
- Can have data of different data types
- Mutable
- `set.add(data)` and `set.remove(data)`
	- `set.append()` will not work because it works on indexed or ordered data only.
- `set.clear()` - no arguments needed, empty the whole set or deletes all the items in the set.
- `set1.union(set2)` - merge both sets omitting the duplicate values.
- `set1.difference(set2)` - only returns the set with the data that is present in set1 and not in set2, hence the data that is unique in set1

### Dictionaries
- Any kind of immutable data type can be used as keys and for values, any data type can be used.
- Values with duplicate keys will be overwritten.
```python
data = {
	"name":"something",
	"class":4,
	"class",6
}

print(data["class"])     # 6
print(data.get("class")) # 6

data.keys()              
data.values()
# all keys and values in a view object which can be converted into list

data.items()  # all the data as key:value pairs

data["new key"] = "new value"
# a new key and value or basically a new data can be assigned like this

# to change the data of a key
data["key"] = "value"
data.update({"key":"value"}) # the argument must be dictionary
# if the dictionary in the above argument has new key with value, it will added

data.pop("key")

"something" in data # by default, it will check in the keys, hence data.keys()
"something" in data.values()
# same logic as above for iterations or loops as well

```

### Exception Handling
**Bugs:** Mistake in code that does not stop the program from completion but leads to unwanted/unexpected or wrong result or behavior.
**Exception:** Mistakes that interrupts the code from executing at the first encountered.

##### Some Exceptions
- `NameError` - Unknown variable is used.
- `SyntaxError` - missing punctuation, missing dot or unclosed bracket, etc.
- `IndexError` - Using index outside of the valid range.
- `TypeError` - Function is called on the wrong data type.
	- When the source of exception or error is from the function itself, such as trying to mutate the elements in tuple. You are trying to do a function which is which cannot be proceeded so a type error.
- `ValueError` - When the value is unacceptable. `int("112A")`
	- When the function is not raising the error but the way you have provided it, the value is raising the error, hence value error.

```python
try:
	# CODE HERE 
except ERROR:
	# CODE HERE
except ERROR:
	# CODE HERE
except ERROR:
	# CODE HERE
```

The code block that might throw an error will be under try and if the mentioned ERROR happened, the execution will not stop and the code block under the except will be executed.

Add all the exceptions that might arise during the execution of the try block, in more except block

The below code will catch any kind of exception as the kind of exceptions is not defined.
```python
try:
	# CODE HERE
except:
	# CODE HERE
```

In the below code, even if the exception is occurred or not, the code under the finally will run for sure.

```python
try:
	# CODE HERE
except ERROR:
	# CODE HERE
finally:
	# CODE HERE
```

In the below code, if there are no exception occurred during the execution of the try block, the code under the else block will be executed, only if the there is no exception
```python
try:
	# CODE HERE
except ERROR:
	# CODE HERE
else:
	# CODE HERE
```

You can raise exceptions by your own if you want to.
```python
if x != "demanded value":
	raise ValueError("description to display in the terminal however not necessary")

# YOU CAN make your custom Error(s) as well by subclassing the python's Exception class. LEARN about it when needed.
```

### Functional Programming
```python
def function():
	# SOME CODE

var1 = function
var2 = function()

def function_with_default_values_for_parameters(a, b = 10):
	# if a is not passed, it will be error, If b is not passed, 10 will be taken as the value of b

# var1 stores the function and function can be called using var1()
# so it is basically like an alias

# var2 executes the function and store the return value
# None if there is no return 

# functions can be used as a argument for other functions as well
# FUNCTIONS THAT TAKE FUNCTIONS AS ARGUMENTS are called HIGHER ORDER FUNCTIONS, they are used for processing various functions and get specific result, they are return functions

# PURE FUNCTION: that gives the same result(s) for the same input(s) and it does not affect anything outside the function, it means it does not do anything outside the function, printing or anything such as modifying the global variables is also NOT DONE by this function. It does not affect the extenal world in the slightest.
# SIMILARLY, if the function is depended on the something external other than the arguments given, such as global variables or input() from the console, it will lead to function being IMPURE FUNCTION as it is interacting, changing or depending on the extenal environment.
```

### Lambda Expression
Allows to make compact functions without needing the formal structure of function definition.

They are functions without a name, created to do something quick and small and simple task.

Also known as anonymous functions as they do not have a name.
```python
greet = lambda name: "Welcome, " + name
print(greet("name"))

lambda argument: expression
lambda price: price * 0.9
# expresson perform a single task and return a result

# as in the first line, a name is assigned to the function hence can be called as a regular function

# they can also take multiple arguments
lambda a, b: a * b
```

The power of lambda functions is explained or can be seen when working with data manipulation and transformation.

**map():** Applies a specified function to every element in an iterable. It provide a result that can be converted into using **list()** for easy viewing and further use.
```python
lower_names = ['apple', 'banana', 'catpucchin', 'dangerous']

def to_upper(name):
	return name.upper()

# first is function and 2nd argument is iterable
converted_to_upper = map(to_upper, lower_names) # all the elements of lower_names will be passed as arguments to to_upper function

converted_to_upper = list(converted_to_upper)


# a better way for above
converted_to_upper = list(map(to_upper, lower_names))

print(converted_to_upper)




# LAMBDA EXPRESSIONS CAN BE USED ABOVE TO OMIT THE NEED TO DEFINING A NEW FUNCTION
converted_to_upper = list(map(lambda name: name.upper(), lower_names))

```

**filter():** almost similar to map() but map() executes a function on all the elements of the iterable, filter() passes the elements through a conditional and if the conditional returns true, only that element will be returned from the filter function. Useful for extraction of the data with a certain condition or criteria.
```python
numbers = [1, 2, 3, 4, 5, 6]

filtered_data = list(filter(lambda num: num % 2 == 0, numbers))

print(filtered_data) # [2, 4, 6]
```

### \*args and \*\*kwargs

**\*args:** allows you to provide any number of arguments before calling the function. It converts all the arguments into a iterable(tuple).

**\*\*kwargs:** allows to provide any number of arguments and they will be converted into the key-value pairs iterables.


> [!NOTE] Remember
> args and kwargs are just terms, they are not static words, ***the main player here is \* and \*\* which is unpacking operator.*** 
> It converts the unknown number of arguments into an iterable, either a ordered iterable(tuple) or key value pair iterable(dictionary)
****

```python
def total(*numbers):
    return sum(numbers)

print(total(1,2,23,12,312,312,31,23,123,12,3)) # 854
```

Here, all the arguments are converted into a tuple and assigned to numbers.

```python
def function(argument1, argument2, *unknown_arguments):
	# code here

# THE FUNCTION will have at least 2 arguments to execute and all the other will be assigned to the unknown_arguments.
# The static or fixed arguments but be written before the unpacking operator.
```

The first line that contains the name and arguments of the function is known as **function signature**

### Decorators
Special functions that modify or enhance other functions.
They basically takes a function as argument, make some changes and return the same function again.
```python
def decorator(func):
	# code here
		
@decorator
def some_func():
	# code here
	return #code here


# The above is basically like 
decorator(some_func)

# it is a good practice to have 'decorator' in the decorator function
```

###### Perfect Example
```python
def greet_decorator(func):
    def wrapper():
        print("Hello!")   # extra code before
        func()            # call the original function
        print("Goodbye!") # extra code after
    return wrapper

@greet_decorator
def say_name():
    print("I’m Buddy!")

say_name()

```

- Python defines the decorator
	- `greet_decorator` is defined — no execution yet.

- Python reaches `@greet_decorator`
	- It immediately executes `say_name = greet_decorator(say_name)`.
	- Inside `greet_decorator`:
		- The original `say_name` is passed as the `func` argument.
		- The inner function `wrapper` is defined (but not run/executed yet).
		- `wrapper` closes over `func` (remembers it).
			- Makes a unique instance of the `wrapper` in the backend and assigns(alias's) it to the host function or the `func`(`say_name()` in this case)
		- Then `wrapper` is returned.

- After returning:
	- `say_name` now points to that returned wrapper.

- So yes — effectively: `say_name = wrapper`
	- (But this wrapper is a unique instance of the inner function that remembers its own func.)

- When you call `say_name()`:
	- **You’re calling that specific wrapper instance.**

- It prints "Hello!", runs the remembered `func()` (the original `say_name`), then prints "Goodbye!".
###### Perfect Example (Stacked Decorators)
```python
def outer_decorator(func):
    def outer_wrapper():
        print(">>> Entering outer layer")
        func()
        print("<<< Exiting outer layer")
    return outer_wrapper

def inner_decorator(func):
    def inner_wrapper():
        print(">>> Entering inner layer")
        func()
        print("<<< Exiting inner layer")
    return inner_wrapper

@outer_decorator
@inner_decorator
def main_task():
    print("Performing main task...")

main_task()
```
- **Python defines** both decorators
    - `outer_decorator` and `inner_decorator` are just stored — no execution yet.

- **Python reaches the decorator assignment**
	- `@outer_decorator` (top)
    - `@inner_decorator` (bottom)
    - The **bottom decorator runs first**.

- ⚙ Inner Decorator
- Executes `inner_decorator(main_task)`.
    - `func` → original `main_task`.
    - Defines `inner_wrapper`.
    - Returns `inner_wrapper`.
- NOW
> `main_task = inner_wrapper` (a unique instance that remembers the original `main_task`).

-  ⚙ Outer Decorator
- Executes `outer_decorator(inner_wrapper)`.
    - `func` → the `inner_wrapper` (returned from previous step).
    - Defines `outer_wrapper`.
    - Returns `outer_wrapper`.
- Now:  
> `main_task = outer_wrapper`.  

▶ When `main_task()` is called:
- Python calls `outer_wrapper()`
    - Prints `>>> Entering outer layer`
    - Calls `func()` → that’s `inner_wrapper`
        - Prints `>>> Entering inner layer`    
        - Calls `func()` → original `main_task`    
            - Prints `Performing main task...`        
        - Prints `<<< Exiting inner layer`    
    - Prints `<<< Exiting outer layer

### OOP 
- Classes - Blueprints
- Objects - Instances of Blueprints
- Attributes - Variables(data/properties) that belong to a object, set during the creation/instantiation of the object and define its state/characteristics.
	- 
```python
# define the name of the class
class ClassName:
	# function that is executed at the time of the creation of the instance
	def __init__(self, attribute_1, attribute_2): # self refers to the instance of the class being created
		# whatever the arguments/attributes passed during the creation process, it will be assigned to that instance of the class
		self.attribute_1 = attribute_1
		self.attribute_2 = attribute_2
	
	# custom functions(known as methods) to give some behavior 
	# self parameter is used so that it can interact with the instance of the class
	def some_function(self):
		# CODE HERE

# creating the object
object_var = ClassName("attribute_1", "property_2")

# accessing the attributes of the created object
print(object_var.attribute_1)

# accessing or using the method/function of the class
object_var.some_function()
```

###### Functions vs Methods
**Functions** are independent and can be called on their own but **Methods** can only be called via an instance of that class in which the method is defined.

#### Inheritance, Polymorphism and Encapsulation
The concept which allows to create new classes with the properties of some existing classes. 
It is used when you want to have a class with its unique properties and some properties which are being inherited from other class as well.

The one which is inheriting the properties is known as **Subclass** or **Child class** and the one whose properties are being inherited is known as **Superclass** or **Parent Class**

In the below example, the `Dog` and `Cat`, both classes have the behavior/method `Moving()`, but only Dog class can `Bark()` and only Cat class can `meow()`.

```python
class Animal:
    def __init__(self):
        pass
    
    def can_move(self):
	    # instance of the class >>> go to the class that created the instance >>> get of the value of its name attribute
        print(self.__class__.__name__ + " can move")
    
class Dog(Animal):
    def bark(self):
        print("I can bark, cannot meow")

class Cat(Animal):
    def meow(self):
        print('I can Meow, cannot bark')

my_dog = Dog()
my_cat = Cat()

my_dog.can_move()
my_dog.bark()
my_cat.can_move()
my_cat.meow()
```

The child class inherits all the attributes and methods of the parent class.
```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def can_move(self):
        print("Can Move")
    
class Dog(Animal):
    def __init__(self, name, breed, height):
	    # by default, using a __init__() in subclass, overrides the init of superclass
	    # # # the new attributes will be set and parent class attribute will be skipped
	    # # # so even though the inheritence will be there, init will not be inherited
	    # if you want to use the attributes of the init class of parent class as well as new attributes for that class, super() is basically used to access the parent class or superclass
        super().__init__(name)
        self.breed = breed
        self.height = height

    def bark(self):
	    # to call a superclass's method in the child's class
	    super().can_move()
        print("I can bark, cannot meow")

# if the method is same in both, child and parent class, the child class's method will override the parent class's method.

```

**Polymorphism:** When the subclass(s) and superclass have same method name, the subclass's method will override the superclass behavior. Hence different class can respond to same methods in their own way.
```python
class Animal:
    def speak(self):
        print("Some generic sound")

class Dog(Animal):
    def speak(self):
        print("Woof!")

class Cat(Animal):
    def speak(self):
        print("Meow!")

animals = [Dog(), Cat(), Animal()]

for a in animals:
    a.speak()
```
Output will be
```shell
Woof!
Meow!
Some generic sound
```

Can be observed in the above example, the same method, `speak()` is being used with different classes and different classes are responding to it in their own way.

**Encapsulation:** Hiding the internal data and controlling the access to it through methods only. (getters/setters)

```python
class Car:
    def __init__(self, model, year, odometer):
        self.model = model
        self.year = year
        self.odometer = odometer
    
    def describe_car(self):
        print(self.year, self.model)
    
    def read_meter(self):
        print(f"Reading is: {self.odometer}")
    
c = Car("BMW", 2000, 15000)

c.describe_car()
c.read_meter()     # Reading is: 15000 
c.odometer = 10000
c.read_meter()     # Reading is: 10000
```
As can be seen in the above code, the value of odometer can be changed by anyone outside the class, this is a security risk.

**<u>Encapsulation or Data Hiding has TWO LEVELS</u>** 
In the first one, we prefix an attribute with single underscore (\_), which signals that <u>It is meant for the internal use and should be viewed as protected.</u>
```python
class Car:
    def __init__(self, model, year, odometer):
        self.model = model
        self.year = year
        # this is just a convention for the programmer to change the stuff whenever wants to 
        # this can still be access from the outside of the class via instance._attribute
        # this is only for the convention to let the programmer know that this is something which is meant to be protected
        # THIS BASICALLY MAKES THE ATTTRIBUTE PROTECTED
        self._odometer = odometer
    
    def describe_car(self):
        print(self.year, self.model)
    
    def read_meter(self):
        print(f"Reading is: {self._odometer}")
    
c = Car("BMW", 2000, 15000)

c.describe_car()      # 2000 BMW
c.read_meter()        # Reading is: 15000                                  
c.odometer = 20000
c.read_meter()        # Reading is: 15000                                  
c._odometer = 20000
c.read_meter()        # Reading is: 20000        

```

**TO REALLY DO SOME PROTECTION so that it cannot be accessed or changed from the outside of the class instance without the methods**

```python
class Car:
    def __init__(self, model, year, odometer):
        self.model = model
        self.year = year
        # THIS BASICALLY MAKES THE ATTTRIBUTE PRIVATE
        self.__odometer = odometer
    
    def describe_car(self):
        print(self.year, self.model)
    
    def read_meter(self):
        print(f"Reading is: {self.__odometer}")
    
c = Car("BMW", 2000, 15000)

c.describe_car()
c.read_meter()          # Reading is: 15000
c.odometer = 20000
c.read_meter()          # Reading is: 15000
c.__odometer = 20000
c.read_meter()          # Reading is: 15000
# as can be observed that the attribute still not changed and still using the one that was using during the creation of the instance

# this is because
# __ basically leads to name mangling
# internall, __odometer is now actually _Car__odometer
# which can be been seen in the output of the current program below
print(c.__dict__)

# The lines that tried to update the odometer failed in updating the value and new attributes are added which are just there but they are not being displayed or used by any of the methods of the Class
# however, the protected attribute here can still be accessed via _Car__odometer because internally it is name mangled
```

```shell
2000 BMW
Reading is: 15000                                  
Reading is: 15000
Reading is: 15000
{'model': 'BMW', 'year': 2000, '_Car__odometer': 15000, 'odometer': 20000, '__odometer': 20000}
```

The Encapsulation via \_ and \_\_ can also be used with methods of the class.
Protected can be used only by the Superclass and Subclass and Private can be used only within Superclass.

#### Class and Static Methods
###### @classmethod
```python
class Car:
    wheels = 4  # class attribute
    # these are the attributes that are universal to all the instances of the class, so changing this will affect the values to be change in all the instances of the class as well

    def __init__(self, model):
        self.model = model  # instance attribute

    @classmethod
    def change_wheels(cls, new_wheels):
    # the first attribute given here is the class itself
    # this method can be called with the instance or without the instance.
    # when it will be called with an instance, @classmethod just let it to access the class of the instance and put it in the cls
        cls.wheels = new_wheels

# Using classmethod
c1 = Car("BMW")
print(c1.wheels)       # 4

Car.change_wheels(6)   # change class attribute

print(Car.wheels)      # 6
print(c1.wheels)       # 6 (all instances see updated value)

```
###### @staticmethod
```python
class Car:
    wheels = 4

    @staticmethod
    def calculate_mileage(distance, fuel):
        return distance / fuel  # just a utility function

# Calling via class
print(Car.calculate_mileage(300, 10))  # 30.0

# Calling via instance
c1 = Car()
print(c1.calculate_mileage(150, 5))    # 30.0

```
- The main point regarding the static method is that, it cannot access or modify or read any class attribute or any instance's attribute. 
- It is just a normal function placed inside a Car.
- Can be called either via Class or instance.
- Will not access/modify the attributes unless specifically given.

##### REAL LIFE USECASE
```python
class BankAccount:
    interest_rate = 0.05  # class-level attribute, same for all accounts
    accounts_created = 0  # track how many accounts created

    def __init__(self, name, balance):
        self.name = name          # instance attribute
        self.balance = balance    # instance attribute
        BankAccount.accounts_created += 1

    # ✅ Normal instance method
    def deposit(self, amount):
        self.balance += amount
        print(f"{self.name} deposited {amount}. New balance: {self.balance}")

    # ✅ Class method
    @classmethod
    def update_interest_rate(cls, new_rate):
        cls.interest_rate = new_rate
        print(f"Updated interest rate to {cls.interest_rate}")

    # ✅ Static method
    @staticmethod
    def validate_account_number(account_number):
        if len(str(account_number)) == 10 and str(account_number).isdigit():
            print("Valid account number")
            return True
        print("Invalid account number")
        return False

```


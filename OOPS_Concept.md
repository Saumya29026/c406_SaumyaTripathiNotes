# Introduction to OOP
Object-Oriented Programming (OOP) is a programming paradigm that uses objects and classes to structure and organize code. 
It focuses on creating reusable and modular code by encapsulating data (attributes) and behavior (methods) into objects.

## Key Concepts of OOP
- Class: A blueprint for creating objects. It defines the attributes and methods that the objects will have.

- Object: An instance of a class. It contains data and methods defined by the class.

- Encapsulation: The bundling of data and methods that operate on the data within a single unit (class).

- Inheritance: A mechanism that allows a new class to inherit attributes and methods from an existing class.

- Polymorphism: The ability of different classes to be treated as instances of the same class through a common interface.

- Abstraction: The concept of hiding complex implementation details and showing only the necessary features of an object.

# Example of OOP in Python

Example of Object-Oriented Programming (OOP) in Python:

```python
# Define a class
class Dog:
    # Constructor method to initialize attributes
    def __init__(self, name, age):
        self.name = name
        self.age = age

    # Method to display dog's information
    def display_info(self):
        print(f"{self.name} is {self.age} years old.")

    # Method to make the dog bark
    def bark(self):
        print(f"{self.name} says Woof!")

# Create an object of the Dog class
my_dog = Dog("Buddy", 3)

# Access attributes and methods
my_dog.display_info()
my_dog.bark()
```
## Constructor (__init__)
A constructor is a special method in a class that is automatically called when an object is created.

It is used to initialize the attributes of an object.

``` python
class Dog:
    # Constructor
    def __init__(self, name, age):
        self.name = name  # Initialize name
        self.age = age    # Initialize age
        print(f"{self.name} has been created!")

# Create an object
my_dog = Dog("Buddy", 3)
```
## Destructor (__del__)
A destructor is a special method that is automatically called when an object is destroyed.

It is used to clean up resources (e.g., closing files, releasing memory).

``` python
class Dog:
    # Constructor
    def __init__(self, name, age):
        self.name = name
        self.age = age
        print(f"{self.name} has been created!")

    # Destructor
    def __del__(self):
        print(f"{self.name} has been deleted!")

# Create an object
my_dog = Dog("Buddy", 3)

# Delete the object explicitly
del my_dog
```


# File Handling in Python
File handling is an essential part of programming that allows you to read from and write to files. Python provides built-in functions and methods to work with files.

## Key File Handling Operations
- Opening a File: Use the open() function to open a file in different modes (read, write, append, etc.).
- Reading from a File: Use methods like read(), readline(), or readlines() to read data from a file.
- Writing to a File: Use the write() or writelines() methods to write data to a file.
- Closing a File: Always close a file using the close() method to free up resources.


```python
# Writing to a file
with open("example.txt", "w") as file:
    file.write("Hello, World!\n")
    file.write("This is a sample file.\n")

# Reading from a file
with open("example.txt", "r") as file:
    content = file.read()
    print(content)
    # Output:
    # Hello, World!
    # This is a sample file.

# Appending to a file
with open("example.txt", "a") as file:
    file.write("Adding a new line to the file.\n")

# Reading line by line
with open("example.txt", "r") as file:
    for line in file:
        print(line.strip())
    # Output:
    # Hello, World!
    # This is a sample file.
    # Adding a new line to the file.
```
## Try-Except Block
A try-except block is used to handle exceptions (errors) in Python.

It ensures that the program doesn’t crash when an error occurs.

```python
try:
    # Create an object
    my_dog = Dog("Buddy", 3)

    # Access attributes and methods
    my_dog.display_info()  # Output: Buddy is 3 years old.
    my_dog.bark()          # Output: Buddy says Woof!

    # Simulate an error (division by zero)
    print(10 / 0)

except ZeroDivisionError:
    print("Error: Division by zero!")
except Exception as e:
    print(f"An error occurred: {e}")
finally:
    print("This will always execute, regardless of exceptions.")
```

### Note
- Use try to wrap code that might raise an exception.
- Use except to handle specific exceptions (e.g., ZeroDivisionError).
- Use finally to execute code that should always run, even if an exception occurs.

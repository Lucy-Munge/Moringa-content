
# Functions Practice: Building a Calculator


## Introduction 

In this project, you'll create a simple calculator which can perform basic arithmetic operations like addition, subtraction, multiplication, or division depending on the user input.

## Objectives

In this lab you will:

- Use a while loop 
- Incorporate input/output functionality in code to allow for user interaction  
- Declare and use a function with arguments 
- Use break and continue to add control flow to a while loop 



## Approach 

- User chooses the desired operation. Options 1, 2, 3, and 4 are valid options for operations   
- Two numbers are taken and an `if…elif…else` branching is used to execute a particular section 
- Using functions `add()`, `subtract()`, `multiply()`, and `divide()` evaluate respective operations 
- The code should handle exceptions and must return **"invalid input"** when an unexpected character is given in the input (anything other than 1 - 4) 

## Example interface
Here is the interface you are expected to build. Don't worry if it is not 100% the same as what is shown. Focus more on the getting the logic correct at this stage. 

```
Please select an operation:
1. Add
2. Subtract
3. Multiply
4. Divide

Select operations from 1, 2, 3, 4 : 1
Enter first number : 20
Enter second number : 13
20 + 13 = 33
```

## Creating arithmetic functions

We'll create four functions, one for each arithmetic operation which will perform the required operation and return the resulting value as shown below:


```python
# Function to add two numbers 
def add(num1, num2):
    # Perform the calculation
    return None
```


```python
# Function to subtract two numbers 
def subtract(num1, num2):
    # Perform the calculation
    return None
```


```python
# Function to multiply two numbers
def multiply(num1, num2):
    # Perform the calculation
    return None
```


```python
# Function to divide two numbers
def divide(num1, num2):
    # Perform the calculation
    return None
```

## Create a command-line user interface
We'll now write the main program body to take user input and call the relevant function:


```python
# Print user menu 


# Take input from the user for operation, followed by numbers  


# Based on operation, pass the two numbers to respective function
# Print the output in a nice manner
# Print "Invalid input" if an unexpected character is seen in input


# Expected output    

# Please select operation -
# 1. Add
# 2. Subtract
# 3. Multiply
# 4. Divide

# Select operations from 1, 2, 3, 4 :1
# Enter first number: 2
# Enter second number: 3
# 2 + 3 = 5
```

Please select operation -
1. Add
2. Subtract
3. Multiply
4. Divide

Select operations from 1, 2, 3, 4 :1    
Enter first number: 2    
Enter second number: 3    
2 + 3 = 5 

## Bring in the `while` loop

We can see how the logic set by using `if-else` statements, along with functions can be used to control the flow of the program in an easy way. Let's add more functionality to our calculator as below:

> Let's try to make it a bit more interesting by introducing the behaviour of a real calculator so our users can choose to either continue with calculations OR exit the system. Users gets this functionality by pressing `y` for yes and `n` for no towards continuation.

## Example interface

**Notice `continue: y/n` at the bottom of interface.**

```
Please select an operation:
1. Add
2. Subtract
3. Multiply
4. Divide

Select operations from 1, 2, 3, 4 : 1
Enter first number : 20
Enter second number : 13
20 + 13 = 33

Continue: y/n
```

Let's work towards implementing iteration into the equation and enclose above I/O interface inside a `while` loop.


```python
# Initialize the code with cont (continue) flag set to yes (y)


# Check for user input after each iteration of the code in a while loop


        # Enclose the I/O  code block inside the while loop
        


# Expected output format

# Select operations from 1, 2, 3, 4 :4
# Enter first number: 5
# Enter second number: 4
# Press d for division and m for modulo operator :m
# 5 / 4 = 1
# Continue? y/n:y
# Select operations from 1, 2, 3, 4 :4
# Enter first number: 5
# Enter second number: 4
# Press d for division and m for modulo operator :d
# 5 / 4 = 1.25
```

## Level up (Optional)

The `while` loop shown above allows the iteration through the code until a specific input from user i.e. `n` is noticed. Let's add some more functionality to this code by asking users about the type of division they are interested in, and this could be either normal division (as before) or a modulo operator (shows remainder).

> Change the code in the division function so that if a user selects division operation, the code should ask the user if they want a normal division `/` or floor division `//`, or a modulo division `%` which only returns the remainder of a division. The program should return an exception for any other inputs. 


```python
def divide_v2(num1, num2):
    # Perform the calculation
    return None
```

## Summary

In this lab, we saw how loops and conditions can be used to control the logic of a program execution based on user input. We started with building a simple calculator and incrementally added more functionality to it by adding loops for iteration and further conditions allowing different types of calculations. We also practiced user I/O by taking choices from the users and dealing with exceptions (unexpected input). 

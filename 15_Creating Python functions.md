# 15. Creating Python packages

Python's power lies in its extensibility through custom components. This section will cover how to create reusable code pieces, from simple functions to complete packages that others can install. Understanding these concepts is crucial for developing maintainable and scalable software solutions in medical and bioinformatics applications.

## 15.1. Custom functions in Python 

**(a) Basic function structure**

You have seen these before so we are just reviewing the fundamentals. 

Functions are the building blocks of modular code, allowing us to encapsulate specific operations for reuse. They help maintain code organization and reduce redundancy in our programs.

The syntax is as below. _Rememeber that although the Docstring is optional, it is very useful to explain what the codes are for_

```
def function_name(parameters):
    """Docstring explaining function purpose and parameters"""
    # Function body
    return result
```

For example,

```
def calculate_bmi(weight_kg, height_m):
    """
    Calculate Body Mass Index (BMI)
    Args:
        weight_kg (float): Weight in kilograms
        height_m (float): Height in meters
    Returns:
        float: BMI value
    """
    return weight_kg / (height_m ** 2)
```

**(b) Advanced function concepts**

Remember that functions can take different types of arguments. These different types are

- **Required positional arguments (positional)**:
- 
These are regular arguments that must be provided when calling the function, in the correct order. For example:

```
def greet(name, age):  # name and age are required positional arguments
    print(f"Hello {name}, you are {age} years old")

greet("Alice", 25)     # Must provide both arguments in correct order
```


- **Variable positional arguments (*args)***:
  
The *args parameter allows a function to accept any number of positional arguments. They are collected into a **tuple**. The name "args" is conventional but you can use any valid name. For example:

```
def sum_numbers(*numbers):  # accepts any number of arguments
    return sum(numbers)

print(sum_numbers(1, 2, 3, 4)) 
print(sum_numbers(10, 20))      
```
  
- **Default parameters (default_param)**:

These are parameters that have a predefined value if no argument is provided. For example:

```
def greet(name, greeting="Hello"):      # greeting has a default value
    print(f"{greeting}, {name}")

greet("Alice")                          # Uses default greeting "Hello"
greet("Bob", "Hi there")                # Uses provided greeting
```

- **Variable keyword arguments (**kwargs)****:

The **kwargs parameter allows a function to accept any number of keyword arguments. They are collected into a **dictionary**. Like args, "kwargs" is conventional but you can use any valid name. For example:

```
def print_user_info(**info):
    for key, value in info.items():
        print(f"{key}: {value}")

print_user_info(name="Alice", age=25, city="New York")
```

Here is an example that combine all together:

```
def process_patient_info(patient_id, *symptoms, status="stable", **medical_data):
    print(f"Patient ID: {patient_id}")
    print(f"Reported Symptoms: {symptoms}")
    print(f"Patient Status: {status}")
    print(f"Additional Medical Data: {medical_data}")

# Using the function with sample medical data
process_patient_info(
    "P12345",                          # Required patient ID
    "fever", "cough", "fatigue",       # Variable number of symptoms
    status="critical",                 # Override default status
    blood_pressure="140/90",           # Additional medical data as keyword arguments
    heart_rate=85,
    o2_saturation=98,
    temperature=38.5
)
```





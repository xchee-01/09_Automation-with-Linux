# 16 Creating Python modules

A module in Python is a file containing Python code that can be reused across different programs. You can think of it as a collection of related functions, classes, and variables that serve a common purpose.

## 16.1. Creating a simple module

Let's create a python module. You may create this using `vim` on Linux and save this module as `patient_vitals.py`. I did not include docstring here for clarity. 

```
def calculate_bmi(weight_kg, height_m):
    return weight_kg / (height_m ** 2)

def classify_bmi(bmi):
    if bmi < 18.5:
        return "Underweight"
    elif 18.5 <= bmi < 25:
        return "Normal weight"
    elif 25 <= bmi < 30:
        return "Overweight"
    else:
        return "Obese"
```

You can then run this using Python. 

1. On your linux terminal, type Python. This should bring you to the python interpreter.

2. You can run the code below **line by line** (meaning, you run each line one at a time)

```
from patient_vitals import calculate_bmi, classify_bmi
weight = 70        # kg
height = 1.75      # meters

bmi = calculate_bmi(weight, height)
print(bmi)

classification = classify_bmi(bmi)
print(classification)
```

## 16.2. Creating a module using `class`

A class is like a blueprint or template for creating objects that have both data (attributes) and functions (methods) bundled together. Let's break it down step by step:

The basic of the class structure is as follows. You can save this as "cat_script.py"

```
class Cat:          # Class names are normally capitalized on the first letter
    # Constructor (initializes a new instance)
    def __init__(self, name, age):
        self.name = name  # Instance variables (attributes)
        self.age = age
    
    # Method (function inside a class)
    def meow(self):
        return f"{self.name} says meow!"
```

Here are some of the key concepts in a class:

- `class`: The keyword to define a class

This is like saying "I'm creating a blueprint for all cats". Just like how all cats share certain characteristics, this blueprint will define what every cat can have and do


- `__init__`: Special method (constructor) that runs when creating a new instance

This is the "setup" function that runs when you create a new cat
__init__ is always called automatically when you make a new cat
The parameters name and age are what you need to provide when creating a cat

- `self`: Refers to the instance being created/used. It is automatically provided in Python. 

`self` means "this specific cat". When you have multiple cats, self helps distinguish between them. It's like saying "THIS cat's name" vs "THAT cat's name"

- Instance variables: Data stored in each instance (like name, age)

These are characteristics that belong to each individual cat
`self.name` stores the name for this specific cat
`self.age` stores the age for this specific cat
Every cat will have its own name and age

- Methods: Functions that belong to the class

These are actions that the cat can do
Methods are just functions that belong to the class

So, with this class, you can create multiple unique instances (which, in this case means cats with their own name and age. Each cat will have access to all the class methods (like meow()), but with their own specific data. It's like having a cat factory where each cat follows the same blueprint but has its own individual characteristics.

So in this case, you can use the modules like this. 

```
import cat_script    # * means import everything

# Creating multiple cats
buddy = cat_script.cat("Buddy", 3)
max = cat_script.cat("Max", 5)
luna = cat_script.cat("Luna", 2)

# Each cat has its own name and age
print(buddy.name)  
print(max.age)     
print(luna.meow()) 

# They're separate instances
print(buddy.name) 
print(max.name)    
```

Do you see the resemblance here when you are using the `pandas` library?

You would first do:

```
import pandas as pd

df = pd.DataFrame(data = d)
```

Alternatively, you can:

```
from cat_script import cat      # Import just the cat class

# Creating multiple cats
buddy = cat("Buddy", 3)
max = cat("Max", 5)
luna = cat("Luna", 2)

# Each cat has its own name and age
print(buddy.name)  
print(max.age)     
print(luna.meow()) 

# They're separate instances
print(buddy.name) 
print(max.name)
```

Going back to our original medical context, you may create a module with the class below:

```
# patient_vitals.py
class Patient:
    def __init__(self, weight_kg, height_m):
        self.weight_kg = weight_kg
        self.height_m = height_m

    def calculate_bmi(self):
        return self.weight_kg / (self.height_m ** 2)

    def classify_bmi(self):
        bmi = self.calculate_bmi()
        
        if bmi < 18.5:
            return "Underweight"
        elif 18.5 <= bmi < 25:
            return "Normal weight"
        elif 25 <= bmi < 30:
            return "Overweight"
        else:
            return "Obese"
```

and use the script as follows in Python (or in another Python script)

```
from patient_vitals import Patient

# Create a patient
patient1 = Patient(70, 1.75)

# Calculate BMI
bmi = patient1.calculate_bmi()
print(f"BMI: {bmi:.1f}")

# Get classification
classification = patient1.classify_bmi()
print(f"Classification: {classification}")
```

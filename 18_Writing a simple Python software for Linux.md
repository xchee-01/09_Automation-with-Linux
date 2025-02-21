# 18. Writing a simple Python software for Linux

## 18.1. Question
With all the knowledge that you have by now on Linux and Python, **use Generative AI** to create a script. 

**Scenario**
You are a software developer at HealthTech Solutions, a healthcare technology company. The company has been contracted by several local clinics to develop a simple command-line tool that helps healthcare providers quickly assess a patient's risk of heart disease based on various health metrics.

**Requirements**
The clinic needs a system that can:

- Calculate heart disease risk based on BMI
- Assess risk based on waist circumference
- Evaluate blood pressure readings considering patient age
- Analyze cholesterol levels (HDL and LDL)
- Consider smoking status in risk assessment
- Combine all these assessments into a single, easy-to-use interface

**Your Task**
Create a set of Python scripts and a bash script that work together to create this risk assessment system. The system should be modular (separate scripts for each assessment) and easy to maintain.

**Technical Requirements**

- Create separate Python scripts for each risk factor assessment
- Use argparse for handling command-line arguments in Python scripts
- Create a bash script that:

(a) Collects patient information
(b) Passes the information to appropriate Python scripts
(c) Displays a comprehensive risk assessment

**Hints for Students**
**Hints**

- Break down the problem into smaller components
- Start with one Python script (e.g., BMI calculator) and test it thoroughly
- Use consistent input/output formats across all scripts
- Use 'read' command to get user input
- Echo blank lines (\n) for better formatting
- Test each Python script separately before combining

## 18.2. Answer

You will need the six scripts below: 

**(a) bmi.py**

```
import argparse

parser = argparse.ArgumentParser()
parser.add_argument('--weight', type=float, required=True)
parser.add_argument('--height', type=float, required=True)
args = parser.parse_args()

bmi = args.weight / (args.height ** 2)

if bmi < 18.5:
    risk = "Low risk of heart disease but underweight"
elif bmi < 25:
    risk = "Normal weight, lower risk of heart disease"
elif bmi < 30:
    risk = "Overweight, increased risk of heart disease"
else:
    risk = "Obese, high risk of heart disease"

print(f"BMI: {bmi:.1f}")
print(f"Risk assessment: {risk}")
```

**(b) waist.py**

```
import argparse

parser = argparse.ArgumentParser()
parser.add_argument('--waist', type=float, required=True)
parser.add_argument('--gender', type=str, required=True)
args = parser.parse_args()

if args.gender.lower() == 'male':
    if args.waist < 94:
        risk = "Low risk of heart disease"
    elif args.waist < 102:
        risk = "Increased risk of heart disease"
    else:
        risk = "High risk of heart disease"
else:
    if args.waist < 80:
        risk = "Low risk of heart disease"
    elif args.waist < 88:
        risk = "Increased risk of heart disease"
    else:
        risk = "High risk of heart disease"

print(f"Waist circumference: {args.waist}cm")
print(f"Risk assessment: {risk}")
```

**(c) blood_pressure.py**

```
import argparse

parser = argparse.ArgumentParser()
parser.add_argument('--systolic', type=int, required=True)
parser.add_argument('--diastolic', type=int, required=True)
parser.add_argument('--age', type=int, required=True)
args = parser.parse_args()

if args.systolic < 120 and args.diastolic < 80:
    risk = "Normal blood pressure, lower risk"
elif args.systolic < 130 and args.diastolic < 80:
    risk = "Elevated blood pressure, moderate risk"
elif args.systolic < 140 or args.diastolic < 90:
    risk = "Stage 1 hypertension, high risk"
else:
    risk = "Stage 2 hypertension, very high risk"

if args.age > 60:
    risk += " (Age is a contributing risk factor)"

print(f"Blood Pressure: {args.systolic}/{args.diastolic}")
print(f"Risk assessment: {risk}")
```

**(d) cholestrol.py**

```
import argparse

parser = argparse.ArgumentParser()
parser.add_argument('--hdl', type=float, required=True)
parser.add_argument('--ldl', type=float, required=True)
args = parser.parse_args()

if args.hdl >= 60:
    hdl_risk = "Good HDL level"
elif args.hdl >= 40:
    hdl_risk = "Borderline HDL level"
else:
    hdl_risk = "Low HDL, increased risk"

if args.ldl < 100:
    ldl_risk = "Optimal LDL level"
elif args.ldl < 130:
    ldl_risk = "Near optimal LDL level"
else:
    ldl_risk = "High LDL, increased risk"

print(f"HDL: {args.hdl} mg/dL - {hdl_risk}")
print(f"LDL: {args.ldl} mg/dL - {ldl_risk}")
```

**(e) smoking.py**

```
import argparse

parser = argparse.ArgumentParser()
parser.add_argument('--smoking_status', type=str, required=True)
args = parser.parse_args()

status = args.smoking_status.lower()

if status == 'never':
    risk = "Lower risk of heart disease"
elif status == 'former':
    risk = "Moderate risk of heart disease, but reduced from when smoking"
elif status == 'current':
    risk = "High risk of heart disease"
else:
    risk = "Invalid smoking status provided"

print(f"Smoking status: {status}")
print(f"Risk assessment: {risk}")
```

**(f) assess_risk.sh**

```
#!/bin/bash

echo "Enter your name:"
read name
echo "Enter your age:"
read age
echo "Enter your weight (kg):"
read weight
echo "Enter your height (m):"
read height
echo "Enter your gender (male/female):"
read gender
echo "Enter your waist circumference (cm):"
read waist
echo "Enter your systolic blood pressure:"
read systolic
echo "Enter your diastolic blood pressure:"
read diastolic
echo "Enter your HDL cholesterol:"
read hdl
echo "Enter your LDL cholesterol:"
read ldl
echo "Enter your smoking status (never/former/current):"
read smoking_status

echo -e "\nRisk Assessment for $name\n"

echo "BMI Assessment:"
python bmi.py --weight $weight --height $height

echo -e "\nWaist Circumference Assessment:"
python waist.py --waist $waist --gender $gender

echo -e "\nBlood Pressure Assessment:"
python blood_pressure.py --systolic $systolic --diastolic $diastolic --age $age

echo -e "\nCholesterol Assessment:"
python cholesterol.py --hdl $hdl --ldl $ldl

echo -e "\nSmoking Risk Assessment:"
python smoking.py --smoking_status $smoking_status
```

## 18.3. Further challenge

Create a zip file containing all these Python scripts and write a shell script that can extract these files, run the risk assessment by collecting user inputs, and clean up afterward. Your solution should work by simply running the shell script, which will handle all the file management and program execution automatically.

**Your solution should produce two files:**

A shell script (launch.sh) that is capable of extracting Python files from a zip file, collecting user inputs for health metrics, running multiple risk assessments, and cleaning up temporary files automatically.
A zip file (heart_risk_assessment.zip) that contains five Python scripts: blood_pressure.py (for blood pressure assessment), bmi.py (for BMI calculation), cholesterol.py (for cholesterol level assessment), smoking.py (for smoking risk assessment), and waist.py (for waist circumference analysis).

When executed, this shell script should handle all the file management and run a complete heart disease risk assessment using these Python scripts.

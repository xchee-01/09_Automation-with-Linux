# 17 Running Python Scripts from Linux

## 17.1. Creating a bash script to run Python scripts

Let's create a simple Python script using Linux Terminal. 

```
# Run on Linux Terminal line by line
touch hello.py
echo 'print("Hello world!")' > hello.py
```

You would have created a Python script. 
To run this Python script on Linux terminal, you would:

```
# Run on Linux Terminal
python3 hello.py
```

> [!NOTE]
> Remember you can also use chmod `+x hello.py` to make it executable directly.
> But this is a matter of preference.

Now, let's imagine now you would like to write a bash script to run "hello.py"

```
# Run on Linux Terminal line by line
touch bash_to_run_hello.sh
echo '#!/bin/bash' > bash_to_run_hello.sh
echo 'echo "Starting Python script..."' >> bash_to_run_hello.sh
echo 'python3 hello.py' >> bash_to_run_hello.sh
echo 'echo "Ending Python script..."' >> bash_to_run_hello.sh
```

> [!TIP]
> You may type `more` to view the bash_to_run_hello.sh to make sure you are doing it right. 

To run the bash that **calls** the script, we can type:

```
# Run on Linux Terminal line by line
bash bash_to_run_hello.sh
```

## 17.2. Creating a bash script to run Python scripts using `sys.argv`

What if you would want to use a variable parsed in the bash script into python? 

`sys.argv` is a list that contains the command line arguments passed to a Python script. Here's how it works:

`sys.argv[0]` is always the name of the script itself
`sys.argv[1]` is the first argument after the script name
`sys.argv[2]` is the second argument and so forth.... 


You can create the script below using `touch` or `vim`

```
# Create this Python using touch or vim
# Save as hello.py 
import sys

name = sys.argv[1]        # Get the first command line argument (name)
date = sys.argv[2]        # Get the second command line argument (date)
print(f"Hello, {name}! Today's date is {date}")
```

Next, you should create the shebang file as below:

```
# Create this shebang using touch or vim
# Save as bash_to_run_hello.sh

#!/bin/bash

echo "Please enter your name: "
read name

current_date=$(date +"%B %d, %Y")

echo "Starting Python script..."
python3 hello.py "$name" "$current_date"
echo "Ending Python script..."
```

Run this script using the shebang file. Now you should be able to see that variables stored in the bashscript is passed to the Python script. 

## 17.3. Creating a bash script to run Python scripts using `argparse`

We can use a more sophiscated way called `argparse`. `argparse` is a Python module that makes it easy to write user-friendly command-line interfaces. It automatically generates help messages and handles various argument types and errors.

Create the Python script below

```
# hello.py

import argparse

parser = argparse.ArgumentParser()
parser.add_argument('--name', required=True)
args = parser.parse_args()

# Use the argument
print(f"Hello {args.name}!")
```

You can run this from the Terminal. The command to be used would be:

```
python3 hello.py --name "Xavier Chee"   # put apostrophe if there is space in the name
```

or put into bash script to run

```
#!/bin/bash

echo "Please enter your name: "
read name

echo "Starting Python script..."
python3 hello.py --name "$name"      
echo "Ending Python script..."
```

Now, if you want to use two arguments, name and date, you can modify the script as below:

```
# hello.py

import argparse

parser = argparse.ArgumentParser()
parser.add_argument('--name', required=True)
parser.add_argument('--date', required=True)

args = parser.parse_args()

# Use the argument
print(f"Hello, {args.name}! Today's date is {args.date}")
```

and 

```
#!/bin/bash
echo "Please enter your name: "
read name

current_date=$(date +"%B %d, %Y")

echo "Starting Python script..."
python3 hello.py --name "$name" --date "$current_date"
echo "Ending Python script..."
```

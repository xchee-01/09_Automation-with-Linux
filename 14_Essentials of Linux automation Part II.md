# 14. Essentials of Linux automation Part II

## 14.1. Python installation and management

Python development in Linux requires understanding the basic Linux environment and package management. This section covers the foundational concepts needed before diving into Python-specific tasks

> [!NOTE]
> Before installing Python, it is important to understand how you can install Linux packages using `apt` (advanced package tools)
> 
> The typical syntax to install a package would be
>
> ```
> sudo apt install package_name
> ```

Let's try and install Python in Linux.

```
# Install Python 3
sudo apt install python3

# Install pip (Python package manager)
sudo apt install python3-pip

# Verify installation
python3 --version
pip3 --version
```

We can also install Python build dependencies. Build dependencies in Python are the external packages, libraries, and tools that are required to build, compile, or install a Python project. 

```
# Install build essentials
sudo apt install build-essential
sudo apt install python3-dev
```

## 14.2. Virtual environments

Now, we can set up virtual envrionments for Python. Virtual environments are isolated Python environments that help manage project dependencies.

Virtual environments are important because they:

(a) Isolate dependencies - each project has its own packages, preventing conflicts
(b) Keep system Python clean - won't mess up your global installation
(c) Make projects reproducible - others can recreate exact environment

To create a conda environment, let's do the following codes
I am going to call my environmet `precisionmed`. You can call it however you want. 

For simplicity, pls go to your Linux Desktop. **Check that you are at Desktop** by typing `pwd`

```
# Install venv module
sudo apt install python3-venv

# Create a virtual environment
python3 -m venv <env name>    # For example, python3 -m venv precisionmed

# You can check if your environment has been created
ls <env name>                 # For example, ls precisionmed
```

You should be able to see the following folders/files created in the environment

- `bin`: Contains executable files, including Python interpreter and activation scripts
- `include`: Contains C header files if you install packages that need compilation
- `lib`: Contains Python packages and libraries installed in this environment
- `lib64`: A symlink to lib for 64-bit systems
- `pyvenv.cfg`: Configuration file that stores settings for the virtual environment, like Python version

This structure ensures your virtual environment is self-contained and isolated from the system Python installation. **When you activate this environment, Python will use these directories instead of the system-wide ones.**

Now, we can activate the environment 

```
# Activate virtual environment
source <env name>/bin/activate

# You can set up an alias. Be sure to change your path to the right path
echo "alias precisionmed='source ~/Desktop/<env name>/bin/activate'" >> ~/.bashrc

source ~/.bashrc                 # Reload the .bashrc

```

Once you have successfully activated your environment, you should see a (<env name>) appearing in front of your prompt. 

> [!NOTE]
> You can deactivate the environment when done just by typing `deactivate`.
> But for this exercise, pls keep the environment activated.

## 14.3. Virtual environments

Scientific computing in Python requires specific packages. You have come across some of these packages before. So lets try and install some of these core packages into our environment. 

**Before we do this, make sure that your environment is activated**

```
# Install packages
pip install pandas numpy scipy matplotlib seaborn
```

You can view the packages installed by going into `<path before>/<env name>/lib/python3.12`. For example, `/home/xavierchee/Desktop/precisionmed/lib/python3.12`

You may also create a requirement files by using this command

```
pip freeze > requirements.txt
```

> [!NOTE] 
> You should see the requirement.txt file being created.
>
> This is very > useful because you can just pass the requirement file to someone to install using the following command `pip install -r requirements.txt`






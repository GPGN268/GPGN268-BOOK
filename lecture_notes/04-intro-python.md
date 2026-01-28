
# Introduction to Python
## Learning Objectives: 
-   List key characteristics and benefits of using the **Python** language for scientific workflows.
- Work with Python in the command prompt
- Know the concepts of variable, data type, and functions


## What is Python

Python is an easy-to-learn, powerful programming language. It has efficient high-level data structures and a simple but effective approach to object-oriented programming. Python’s elegant syntax and dynamic typing, together with its interpreted nature, make it an ideal language for scripting and rapid application development in many areas on most platforms.

Key Characteristics:

-   **Interpreted Language:** **Python** is an interpreted programming language. At the most basic level, an interpreted language means that you can run **Python** code and associated commands without needing additional steps such as compiling the code first before running it. This makes getting started and working with **Python** quick and easy.
-   **High Level Programming Language:** **Python** is also a high-level programming language, which provides the ability to work with code that is human readable, as opposed to machine language (such as 0s and 1s). As the **Python** language abstracts away many of those technical details, you are free to write code and process data using **Python** without worrying about what type of computer you are using. So you can get more quickly to your science and be able to share your code with others who may be using a different operating system.
-   **Free and Open Source:** **Python** is a free and open source programming language. This means that the source code for the entire language is freely available, and that anyone can contribute new functionality or documentation for the benefit of the **Python** community.


### Why Use Python For Earth Data Science

Each programming language has its benefits and its drawbacks. **Python** is being used in our earth analytics courses and in this textbook for many reasons including:

1.  **Python is one of the most commonly used languages in the earth and environmental sciences:** Many different sources have identified **Python** as being one of the most popularly used languages, particularly in the sciences. [An analysis conducted by Stack Overflow](https://insights.stackoverflow.com/survey/2019) found that **Python** is one of the most active programming language threads on their widely used website and the overall fastest-growing major programming language. Earth Lab’s own [market research of hiring managers in industry and public agencies](https://www.earthdatascience.org/blog/four-skills-earth-data-science/) also identified **Python** as a highly desired programming background for new employees.
2.  **Python is free and open source:** This means that anyone can use it without worrying about licenses. This also makes it easy to migrate code over to cloud and high performance computing (HPC) environments, given that there are no license restrictions.
3.  **Python has an active open source community for science:** There is an active open source community who are building **Python** tools to support scientific applications, such as the widely used scientific packages [numpy](https://github.com/numpy/numpy) and [pandas](https://github.com/pandas-dev/pandas).
4.  **Python is the core language for many spatial data tools:** Example tools that use **Python** as their core include ESRI ArcGIS, QGIS and others. This makes the language versatile if you wish to create macros (i.e. widgets) in a Desktop tool like QGIS.


### Where to run Python

To run python, open your terminal (or GitBash) and run:

```
$ python
```
(Note: your command might be python3m depending on your system.)


## Using Python for the first time
### Variables

Any Python interpreter can be used as a calculator:

```python
3 + 5 * 4
```

```python
23
```

This is great but not very interesting. To do anything useful with data, we need to assign its value to a _variable_. In Python, we can [assign](https://swcarpentry.github.io/python-novice-inflammation/reference.html#assign) a value to a [variable](https://swcarpentry.github.io/python-novice-inflammation/reference.html#variable), using the equals sign `=`. For example, we can track the weight of a patient who weighs 60 kilograms by assigning the value `60` to a variable `weight_kg`:

```python
temperature = 60
```

From now on, whenever we use `temperature`, Python will substitute the value we assigned to it. In layperson’s terms, **a variable is a name for a value**.

In Python, variable names:

-   can include letters, digits, and underscores
-   cannot start with a digit
-   are [case sensitive](https://swcarpentry.github.io/python-novice-inflammation/reference.html#case-sensitive).

This means that, for example:

-   `temperature0` is a valid variable name, whereas `0temperature` is not
-   `temperature` and `Temperature` are different variables

The following identifiers are used as reserved words, or keywords of the language, and cannot be used as ordinary identifiers. They must be spelled exactly as written here:

#### Expressive Programming: Easy to Understand Variable Names Make Your Code Easier to Read

Just like you want to use [expressive naming conventions (names that represent what is stored within the directory)](https://www.earthdatascience.org/courses/intro-to-earth-data-science/open-reproducible-science/get-started-open-reproducible-science/best-practices-for-organizing-open-reproducible-science/) for directories on your computer, you also want to use short, clear names for your variables to make your code easier to read. To follow best practices for variable names, avoid the following:

-   spaces in your variable names
-   complicated wording
-   long variable names
-   words that do not represent what the variable contains (example: `my_variable` vs `precip_data`)

When naming a variable, you want to keep the name short but specific enough that someone reading your code can understand what it contains. It is good practice to use underscores (e.g. `denver_precip_in`) to create multi-word variable names that provide specifics regarding the variable’s content. The underscore makes the variable name easier to read and follows **Python** [PEP 8 best practices for code readability](https://www.python.org/dev/peps/pep-0008/#naming-conventions).

### Types of data

Python knows various types of data. Three common ones are:

-   integer numbers
-   floating point numbers, and
-   strings.

In the example below, variable `temperature` has an integer value of `60`, whereas  `precip` has a float value of  `3.3`.

```python
temperature = 60
```

```python
precip = 3.3
```

To create a string, we add single or double quotes around some text. 

```python
city = 'Golden'
```

A string can have many words, including punctuation.

```python
city_description = 
"Golden, CO is the home of Colorado School of Mines."
```


### Built-in Python functions 

To carry out common tasks with data and variables in Python, the language provides us with several built-in [functions](https://swcarpentry.github.io/python-novice-inflammation/reference.html#function). The function ` type` tells what type a certain variable is.
```python
type(temperature)
<class 'int'>
```

When we want to make use of a function, referred to as calling the function, we follow its name by parentheses. The parentheses are important: if you leave them off, the function doesn’t actually run! Sometimes you will include values or variables inside the parentheses for the function to use. In the case of `print`, we use the parentheses to tell the function what value we want to display. We will learn more about how functions work and how to create our own later in the course.

```python
type(precip)
<class 'float'>
```

```python
type(city)
<class 'str'>
```

To display information on the screen, we use the `print` function:

```python
print(temperature)

```

```python
print(city)
```

We can display multiple things at once using only one `print` call:

```python
print("The temperature in", city, "is", temperature)
```


We have been running code in the Python prompt, but what if we need to run this again? If you exit Python (ctrl+d) and launch it again, what happens to your code?

```python
temperature
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'temperature' is not defined
```

Python doesn't "remember" the code that we typed in the command prompt. So how ca we save code such that we can run it later?

Let's open a terminal and navigate to your coursework directory

```
$ cd ~/work/classes/GPGN268/villasboas-coursework/
```

Now, let's go to the `short-assignments` directory.

```
$ cd short-assignments
```

We will create a file to save our code

```
$ vim python-intro.py
```


```python
# Learning how to write a Python script - GPGN268
# Author: Bia Villas Boas
# Date: Jan 31, 2023

# Temperature in degrees Fahrenheit
temperature = 55
# Location of the measurement
city = "Golden"
print("It is", temperature, "F", "in", city)
```

and you can run your script with

```
$ python python-intro.py
```


### Commit your changes

Now let's track the Python script that you created with Git, commit, and push that to GitHub.

```
$ git add python-inyto.py
$ git commit -m "Add my first python script"
$ git push
```


<!-- ## Jupyter Lab

Repeat with me: "Jupyter notebook is not Python"

[JupyterLab](https://jupyterlab.readthedocs.io/) will be our primary method for interacting with the computer. JupyterLab contains a complete environment for interactive scientific computing which runs in your web browser. Jupyter is an open source python project that was started by scientists like yourselves who wanted a more effective way to interact with their computers.

JupyterLab has excellent documentation. Rather than repeat that documentation here, we point you to their docs. The following pages are particularly relevant:

-   [The JupyterLab Interface](https://jupyterlab.readthedocs.io/en/stable/user/interface.html)
    
-   [Working with Files](https://jupyterlab.readthedocs.io/en/stable/user/files.html)
    
-   [The Text Editor](https://jupyterlab.readthedocs.io/en/stable/user/file_editor.html)
    
-   [Notebooks](https://jupyterlab.readthedocs.io/en/stable/user/notebook.html)
    
-   [Terminals](https://jupyterlab.readthedocs.io/en/stable/user/terminal.html)
    
-   [Managing Kernels and Terminals](https://jupyterlab.readthedocs.io/en/stable/user/running.html)
    

You will gain experience and familiarity with JupyterLab over the course of the semester as we use it in our weekly lectures and assignments. -->

## Key Points
- Python is an interpreted, high-level, open-source language widely used in Earth sciences.
- Variables are names assigned to values using `=`; use short, specific names with underscores (e.g., `denver_precip_in`).
- Common data types: integers, floating-point numbers, and strings.
- Built-in functions like `type()` and `print()` help you work with variables.
- Python scripts saved in `.py` files can be run from the terminal using `python filename.py`.
- Use Git to track and version control your Python scripts.

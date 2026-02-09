# Further into Python (conda and Jupyter notebooks)
## Learning Objectives: 
-   Explain what a library is and what libraries are used for.
-   Import a Python library and use the functions it contains.
-   Read tabular data from a file into a program.
-   Select individual values and subsections from data.
-   Perform operations on arrays of data.

## Managing Python Packages using conda
When working with a programming language, such as Python, that can do almost _anything_, one has to wonder how this is possible. If you download Python, it has about 25 MB, how can everything be included in this small data package? The answer is - it is not. Python, as well as many other programming languages, uses external libraries or packages for being able to do almost _anything_. 

A very useful library is called [pandas](https://pandas.pydata.org/), but if we try to import pandas we will get an error
```python
import pandas as pd
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'pandas'
```

`pandas` was not installed, so we need to use a package manager to download and install `pandas` for us.

### Conda
One option for is to manage packages with `conda`. Conda is an open-source package and environment management system that runs on Windows, Mac OS, and Linux.

-   Conda can quickly install, run, and update packages and their dependencies.
-   Conda can create, save, load, and switch between project-specific software environments on your local computer.
-   Although Conda was created for Python programs, Conda can package and distribute software for any language such as R, Ruby, Lua, Scala, Java, JavaScript, C, C++, FORTRAN.

Conda as a _package manager_ helps you find and install packages. Python coupled with a package and environment manager provides a way to make isolated, reproducible _environments_ where you have fine-tuned control over all packages and configurations. **You should always work within an environment**, rather than the “default” environment.

It is strongly recommended to read official [Getting Started with Conda](https://conda.io/docs/user-guide/getting-started.html) guide.

#### Setting up conda
Let's start setting up conda
```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh -b
conda activate
```

You should see `(base)` on front of your prompt. Like
```
(base) ryandu@ryansjduhp:...
```
This is the base environment of conda. 

We would like to create a new envrionment for each "project" we are on, so that the python environment we use is clean and minimal (a large and complicated environment is slow to manipulate). This also decrese the chance that the packages are in conflict with each other.

For this we create a conda environment names GPGN268:
```
conda create -n GPGN268 -y
conda activate GPGN268
```
Now we can install packages we wish to used inside the conda environment. This will only make these packages available inside the environment GPGN268. We will first install packages for running jupyter notebook
```
conda install jupyter ipykernel -y
```
When you attempt a run a notebook, you should be able to select GPGN268 as the kernel.

#### Further conda commands
You can deactivate your environment by typing:

```
$ conda deactivate
```
To see all the environments on your system:

```
$ conda info --envs
```

If you want to permanently remove an environment and delete all the data associated with it:

```
$ conda remove --name my_environment --all
```

For extensive documentation on using environments, please see [the conda documentation](https://conda.io/docs/using/envs.html). The most important feature to review here is the ability to _share and export_ your environment; this is the basis for reproducibility in the scientific Python stack. At any time from the shell, you can execute

#### Installing More Packages
Once you have a basic Python environment, you can easily add or remove packages using conda. Conda was created to help manage the complex dependencies and pre-compiled binary libraries that are necessary for scientific python.

To install packages, first, you activate the environment that you would like to work on:

```
$ conda activate GPGN268
```

Then, you can install packages from an official, curated set of packages which are built and tested for a number of different system configurations on Linux, Windows, and macOS

```
$ conda install -c conda-forge matplotlib numpy scipy pandas xarray cartopy
```
While conda allows you to install almost any science-related package, there may be other general-use python packages you wish to you that are not available in via conda. For these, you can use an alternative installation method.

Outside of the scientific python community, the most common way to install packages is to search for them on the official [PyPI](https://pypi.python.org/pypi) index. Once you’ve found the package you want to install (you may have also just found it on github or elsewhere), you use the **pip** command from a the command line:

```
$ pip install <package-name>
```

#### Speeding things up with Mamba

In order to put together an actual python environment from your package specifications, conda has to solve a difficult puzzle. Each package specified has certain dependencies on other packages. For example, Xarray depends on Numpy, Pandas, and several others. Moreover, each version of Xarray requires certain minimum versions of other packages (e.g. Xarray 0.19 requires Numpy >= 1.17 and Pandas >= 1.0). Other packages in your environment may have different or incompatible versions. Finding a combination of packages that are mutually compatible can be framed mathematically as a [boolean satisfiability problem](https://en.wikipedia.org/wiki/Boolean_satisfiability_problem).

The default “solver” of this problem for conda can be [slow](https://www.anaconda.com/blog/understanding-and-improving-condas-performance) It is not unheard of to spend 30 minutes or more solving large environments! 😱 

Fortunately, a much faster alternative called [mamba](https://github.com/mamba-org/mamba) has recently come out. To install it, just run:

```
$ conda install -c conda-forge mamba
```

Now you can install environments and packages as before, but using the `mamba` command instead of `conda`. Everything will be faster.


## Jupyter notebooks in VS Code, and the conda environment
Jupyter notebook will be our primary method for interacting with the computer. Jupyter is an open source python project that was started by scientists like yourselves who wanted a more effective way to interact with their computers. Notebooks are useful tools for sharing scientific data analysis codes and figures.

Visual Studio Code (VS Code) is one of the many integrated development environment (IDE) available (you are welcome to explore others). We will use it to open and edit Jupyter Notebook files. Alternativelty, one can use the browser to interact with Jupyter Lab. 

### Setting up
If you type `code .` in your terminal, VSCode will appear already running inside of WSL (for windonws user). It will also open the folder you typed `code .` from. 

Once you open a Notebook, on the top right corner you can select the python kernel it will use. You should select the conda environment we created called `GPGN268`. 

## Writing a notebook
### Some more setting up
Create a directory for the intro to Python  module
```
cd ~/work/classes/GPGN268/coursework-du
mkdir -p ds00-python-intro/data
mkdir -p ds00-python-intro/notebooks
```
Getting the data for today's class
```
cd ~/work/classes/GPGN268/
git clone git@github.com:GPGN268/GPGN268-CORE.git
cd GPGN268-CORE
git pull
```

```
ls -RF
```

```
cd intro-python/data
ls -F
```

```
cp meteo*.txt ~/work/classes/GPGN268/coursework-du/ds00-python-intro/data
```

Now let's navigate to our newly created directory 
```
cd ~/work/classes/GPGN268/coursework-du/ds00-python-intro
```
And launch VSCode.

### Loading data into Python
First lets add a Markdown header so we know what this notebook is about.

```markdown
# GPGN268 - Introduction to Python
**Author:** Bia Villas Boas

This notebook uses meteorological data from the Denver water department to introduce basic Python concepts.
```

We would like to process the Denver meteorological data using Python. But what is actually in these files? Let's use the terminal (or text editor) to take a look at the files using an additional tab  in VSCode. It looks like these files have numbers that are organized in columns and rows and separated by some white spaces.

To begin processing the meteorological data, we need to load it into Python. We can do that using a library called [NumPy](https://numpy.org/), which stands for Numerical Python. In general, you should use this library when you want to manipulate lots of numbers, especially if you have matrices or arrays. To tell Python that we’d like to start using NumPy, we need to import it:

```python
import numpy as np
```

Importing a library is like getting a piece of lab equipment out of a storage locker and setting it up on the bench. Libraries provide additional functionality to the basic Python package, much like a new piece of equipment adds functionality to a lab space. Just like in the lab, importing too many libraries can sometimes complicate and slow down your programs - so we only import what we need for each program.

Once we’ve imported the library, we can ask the library to read our data file for us:

```python
np.loadtxt(fname='../data/meteo_denver_tmax_2000_2022.txt', delimiter='\t')
```

The expression `numpy.loadtxt(...)` is a [function call](https://swcarpentry.github.io/python-novice-inflammation/reference.html#function-call) that asks Python to run the [function](https://swcarpentry.github.io/python-novice-inflammation/reference.html#function) `loadtxt` which belongs to the `numpy` library. The dot notation in Python is used most of all as an object attribute/property specifier or for invoking its method. `object.property` will give you the object.property value, `object_name.method()` will invoke on object_name method.

As an example, Mines Stadium is the stadium that belongs to Mines. We could use the dot notation to write  `mines.stadium`, just as `loadtxt` is a function that belongs to the `numpy` library.

`numpy.loadtxt` has two [parameters](https://swcarpentry.github.io/python-novice-inflammation/reference.html#parameter): the name of the file we want to read and the [delimiter](https://swcarpentry.github.io/python-novice-inflammation/reference.html#delimiter) that separates values on a line. These both need to be character strings (or [strings](https://swcarpentry.github.io/python-novice-inflammation/reference.html#string) for short), so we put them in quotes.

Since we haven’t told it to do anything else with the function’s output, the [notebook](https://swcarpentry.github.io/python-novice-inflammation/reference.html#notebook) displays it. In this case, that output is the data we just loaded. By default, only a few rows and columns are shown (with `...` to omit elements when displaying big arrays). Note that, to save space when displaying NumPy arrays, Python does not show us trailing zeros, so `1.0` becomes `1.`.

Our call to `numpy.loadtxt` read our file but didn’t save the data in memory. To do that, we need to assign the array to a variable. In a similar manner to how we assign a single value to a variable, we can also assign an array of values to a variable using the same syntax. Let’s re-run `numpy.loadtxt` and save the returned data:

```python
tmax = np.loadtxt(fname='../data/meteo_denver_tmax_2000_2022.txt', delimiter='\t')
```

This statement doesn’t produce any output because we’ve assigned the output to the variable `data`. If we want to check that the data have been loaded, we can type the variable’s name:

```python
tmax
```

Now that the data are in memory, we can manipulate them. First, let’s ask what [type](https://swcarpentry.github.io/python-novice-inflammation/reference.html#type) of thing `data` refers to:

```python
type(tmax)

```

```
<class 'numpy.ndarray'>
```

The output tells us that data currently refers to an N-dimensional array, the functionality for which is provided by the NumPy library. These data correspond to arthritis patients’ inflammation. The rows are the individual patients, and the columns are their daily inflammation measurements.

### Data Type
A Numpy array contains one or more elements of the same type. The type function will only tell you that a variable is a NumPy array but won’t tell you the type of thing inside the array. We can find out the type of the data contained in the NumPy array.

```python
tmax.dtype
```

```
float64
```

This tells us that the NumPy array’s elements are floating-point numbers.

With the following command, we can see the array’s shape:

```python
print(tmax.shape)
```

```
(23, 12)
```

The output tells us that the `tmax` array variable contains 23 rows and 12 columns. When we created the variable `tmax` to store our temperature data, we did not only create the array; we also created information about the array, called [members](https://swcarpentry.github.io/python-novice-inflammation/reference.html#member) or attributes. This extra information describes `tmax` in the same way an adjective describes a noun. `tmax.shape` is an attribute of `tmax` which describes the dimensions of `tmax`. We use the same dotted notation for the attributes of variables that we use for the functions in libraries because they have the same part-and-whole relationship.

If we want to get a single number from the array, we must provide an [index](https://swcarpentry.github.io/python-novice-inflammation/reference.html#index) in square brackets after the variable name, just as we do in math when referring to an element of a matrix. Our inflammation data has two dimensions, so we will need to use two indices to refer to one specific value:

```python
print('first value in tmax:', tmax[0, 0])
```

```python
first value in tmax: 50.9
```

```python
print('middle value in tmax:', tmax[11, 6])
```

```python
middle value in tmax: 92.7
```

The expression `tmax[11, 6]` accesses the element at row 11, column 6. While this expression may not surprise you, `tmax[0, 0]` might. Programming languages like Fortran, MATLAB and R start counting at 1 because that’s what human beings have done for thousands of years. Languages in the C family (including C++, Java, Perl, and Python) count from 0 because it represents an offset from the first value in the array (the second value is offset by one index from the first value). This is closer to the way that computers represent arrays (if you are interested in the historical reasons behind counting indices from zero, you can read [Mike Hoye’s blog post](http://exple.tive.org/blarg/2013/10/22/citation-needed/)). As a result, if we have an M×N array in Python, its indices go from 0 to M-1 on the first axis and 0 to N-1 on the second. It takes a bit of getting used to, but one way to remember the rule is that the index is how many steps we have to take from the start to get the item we want.


### Slicing data

An index like `[11, 6]` selects a single element of an array, but we can select whole sections as well. For example, we can select the first ten days (columns) of values for the first four patients (rows) like this:

```python
tmax[0:4, 0:6]
```

```
array([[50.9, 56.4, 57.5, 69.3, 78.2, 86. ],
       [48.2, 45.4, 54.8, 65.8, 73.8, 87.3],
       [47.7, 51.8, 51.7, 69.7, 73.1, 90.4],
       [54.7, 44.7, 54.6, 67.9, 73.8, 80.1]])
```

The [slice](https://swcarpentry.github.io/python-novice-inflammation/reference.html#slice) `0:4` means, “Start at index 0 and go up to, but not including, index 4”. Again, the up-to-but-not-including takes a bit of getting used to, but the rule is that the difference between the upper and lower bounds is the number of values in the slice.

We don’t have to start slices at 0:

```python
tmax[5:10, 0:6]
```

```
array([[49.2, 51.2, 55.4, 62.5, 73.8, 84.3],
       [54.5, 47.8, 53.5, 68.9, 74.9, 87.1],
       [30.6, 40.8, 58.5, 61.7, 72.5, 86.5],
       [40.1, 48.6, 54.8, 63. , 72.5, 85. ],
       [52. , 56.5, 60.5, 61.2, 73.7, 80.6]])
```

We also don’t have to include the upper and lower bound on the slice. If we don’t include the lower bound, Python uses 0 by default; if we don’t include the upper, the slice runs to the end of the axis, and if we don’t include either (i.e., if we use ‘:’ on its own), the slice includes everything:

```python
subset = python[:3, 6:]
print('subset is:')
print(subset)
```

The above example selects rows 0 through 2 and columns 36 through to the end of the array.

```
subset is:
[[94.7 93.  81.9 67.5 46.2 46.1]
 [95.3 90.6 86.  69.7 61.7 50.2]
 [96.  90.3 82.  63.3 52.3 50.6]]
```

### Analyzing data

NumPy has several useful functions that take an array as input to perform operations on its values. If we want to find the average inflammation for all patients on all days, for example, we can ask NumPy to compute `tmax`’s mean value:

```python
np.mean(tmax)
```

```
67.9909420289855
```

`mean` is a [function](https://swcarpentry.github.io/python-novice-inflammation/reference.html#function) that takes an array as an [argument](https://swcarpentry.github.io/python-novice-inflammation/reference.html#argument).

Let’s use three other NumPy functions to get some descriptive values about the dataset. We’ll also use multiple assignment, a convenient Python feature that will enable us to do this all in one line.

```python
maxval, minval, stdval = np.max(tmax), np.min(tmax), np.std(tmax)

print('maximum max temperature:', maxval)
print('minimum max temperature:', minval)
print('standard deviation:', stdval)
```

Here we’ve assigned the return value from `np.max(tmax)` to the variable `maxval`, the value from `numpy.min(tmax)` to `minval`, and so on.

```python
maximum max temperature: 96.7
minimum max temperature: 30.6
standard deviation: 16.614984435991314
```


> #### Mystery Functions in IPython[](https://swcarpentry.github.io/python-novice-inflammation/02-numpy/index.html#mystery-functions-in-ipython)
> 
> How did we know what functions NumPy has and how to use them? If you are working in IPython or in a Jupyter Notebook, there is an easy way to find out. If you type the name of something followed by a dot, then you can use [tab completion](https://swcarpentry.github.io/python-novice-inflammation/reference.html#tab-completion) (e.g. type `numpy.` and then press Tab) to see a list of all functions and attributes that you can use. After selecting one, you can also add a question mark (e.g. `numpy.cumprod?`), and IPython will return an explanation of the method! This is the same as doing `help(numpy.cumprod)`. Similarly, if you are using the “plain vanilla” Python interpreter, you can type `numpy.` and press the Tab key twice for a listing of what is available. You can then use the `help()` function to see an explanation of the function you’re interested in, for example: `help(numpy.cumprod)`.

When analyzing data, though, we often want to look at variations in statistical values, such as the maximum max temperature per year or the average max temperature per month. One way to do this is to create a new temporary array of the data we want, then ask it to do the calculation:

```python
tmax_2000 = tmax[0, :] # 0 on the first axis (rows), everything on the second (columns)
print('maximum temperature in 2000:', np.max(tmax_2000))
```

```
maximum temperature in 2000: 94.7
```

Everything in a line of code following the ‘#’ symbol is a [comment](https://swcarpentry.github.io/python-novice-inflammation/reference.html#comment) that is ignored by Python. Comments allow programmers to leave explanatory notes for other programmers or their future selves.

We don’t actually need to store the row in a variable of its own. Instead, we can combine the selection and the function call:

```
print('maximum temperature in 2002:', np.max(tmax[2, :]))
```

```
maximum temperature in 2002: 96.0
```

What if we need the maximum temperature for each year over all months (as in the next diagram on the left) or the average across all years for each month (as in the diagram on the right)? As the diagram below shows, we want to perform the operation across an axis:

![[array-operations.png]]

To support this functionality, most array functions allow us to specify the axis we want to work on. If we ask for the average across axis 0 (rows in our 2D example), we get:

```python
np.mean(tmax, axis=0)
```

```
array([48.46521739, 47.93913043, 57.72173913, 65.00869565, 72.70434783,
       86.58695652, 92.50869565, 90.35652174, 82.69130435, 67.76956522,
       56.75652174, 47.3826087 ])
```

As a quick check, we can ask this array what its shape is:

```python
np.mean(tmax, axis=0).shape
```

```
(12,)
```

The expression `(12,)` tells us we have an N×1 vector, so this is the average max temperature per month for all years. If we average across axis 1 (columns in our 2D example), we get:

```python
np.tmax(tmax, axis=1)
```

```
array([68.975     , 69.06666667, 68.24166667, 68.34166667, 67.05833333,
       68.20833333, 65.125     , 64.35      , 66.65833333, 66.49166667,
       68.2       , 67.49166667, 71.26666667, 66.96666667, 67.80833333,
       68.59166667, 69.93333333, 69.03333333, 68.74166667, 66.875     ,
       69.14166667, 69.09166667, 68.13333333])

```

which is the average max temperature per year across all months.


### Clear notebook and commit changes

In the VSCode toolbar click on `Kernel` then `Restart Kernel and Clear All Outputs`

Now, in the terminal, add you notebook to git, commit, and push to GitHub.


## Key Points

- Python libraries/packages extend Python's functionality beyond the base installation; they must be imported before use with `import` statements.
- Conda environments provide isolated, reproducible workspaces for different projects; always work within a specific environment rather than the base environment.
- Create environments with `conda create -n <name>`, activate with `conda activate <name>`, and deactivate with `conda deactivate`.
- Install packages using `conda install <package>` (for curated scientific packages) or `pip install <package>` (for general PyPI packages).
- Jupyter notebooks in VS Code allow interactive Python programming.
- NumPy is the fundamental library for numerical computing in Python, providing support for arrays and mathematical operations.
- Array indexing in Python starts at 0 (not 1); access elements with `array[row, column]` syntax.
- Array slicing uses `start:end` notation where the end index is exclusive; omitting bounds defaults to the beginning or end of the array.
- NumPy functions like `np.mean()`, `np.max()`, `np.min()`, and `np.std()` perform operations on arrays; use the `axis` parameter to specify operations along rows (axis=0) or columns (axis=1).
- Comments in Python code start with `#` and are ignored by the interpreter; use them to explain code logic.
- Version control your notebooks by clearing outputs before committing to keep git diffs clean and meaningful.

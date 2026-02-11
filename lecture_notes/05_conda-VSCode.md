# Developing code in Python (conda and VSCode)
## Learning Objectives: 
-   Explain what a library is and what libraries are used for.
-   Import a Python library and use the functions it contains.
-   Be able to set up a conda environment from scratch.
-   Be able to import and export a conda environment.
-   Know what a jupyter notebook is and be able to edit one in VSCode.

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

One option for is to manage packages with `conda`. Conda is an open-source package and environment management system that runs on Windows, Mac OS, and Linux.

-   Conda can quickly install, run, and update packages and their dependencies.
-   Conda can create, save, load, and switch between project-specific software environments on your local computer.
-   Although Conda was created for Python programs, Conda can package and distribute software for any language such as R, Ruby, Lua, Scala, Java, JavaScript, C, C++, FORTRAN.

Conda as a _package manager_ helps you find and install packages. Python coupled with a package and environment manager provides a way to make isolated, reproducible _environments_ where you have fine-tuned control over all packages and configurations. **You should always work within an environment**, rather than the “default” environment.

It is strongly recommended to read official [Getting Started with Conda](https://conda.io/docs/user-guide/getting-started.html) guide.

### Setting up conda
Let's start setting up conda. First, find the script appropriate for you here: https://repo.anaconda.com/miniconda/. Pay attention to your operating system: Linux or MacOSX, and if you are on Mac, if your computer uses an Arm processor.

Now type these into your terminal. You should say yes to all the prompt.
```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
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
conda install jupyter ipykernel
```
When you attempt a run a notebook, you should be able to select GPGN268 as the kernel.

### Further conda commands
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

### Installing More Packages
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

### Exporting and importing your conda environment
Conda allows you to share your environment with other people in a compact way. You can export your conda environment. Make sure you are in the `GPGN268` conda environment, and in a folder like `coursework-lastname`, type
```
conda env export --no-builds --from-history > environment.yml
```
You can see that now you have a file in `coursework-lastname` that saves what packages you installed in `GPGN268` conda environment. You can share this file with the public in Github so that others have an easier time reproducing your python environment.

To impoart from a `.yml` file, use
```
conda env create -f environment.yml
```

### Speeding things up with Mamba

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

## Key Points

- Python libraries/packages extend Python's functionality beyond the base installation; they must be imported before use with `import` statements.
- Conda environments provide isolated, reproducible workspaces for different projects; always work within a specific environment rather than the base environment.
- Create environments with `conda create -n <name>`, activate with `conda activate <name>`, and deactivate with `conda deactivate`.
- Install packages using `conda install <package>` (for curated scientific packages) or `pip install <package>` (for general PyPI packages).
- You can share your conda environment and import from one other has shared.
- Jupyter notebooks in VS Code allow interactive Python programming.

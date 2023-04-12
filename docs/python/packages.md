# Packages

!!! info "Python packages"
    - Python **packages broaden the use of python** to almost infinity! 
    - Instead of writing code yourself there may be others that have done the
      same!
    - Many **scientific tools** are distributed as **python packages**, making
      it possible to run a script in the prompt and there define files to be
      analysed and arguments defining exactly what to do.
    - A nice **introduction to packages** can be found here:
      https://aaltoscicomp.github.io/python-for-scicomp/dependencies/ 

!!! question
    - How do I find which packages and versions are available?
    - What to do if I need other packages?
   
There are two package installation systems:

- **PyPI** (``pip``) is traditionally for Python-only packages but it is no problem to also distribute packages written in other languages as long as they provide a Python interface.
- **Conda** (``conda``) is more general and while it contains many Python packages and packages with a Python interface, it is often used to also distribute packages which do not contain any Python (e.g. C or C++ packages).
    - Creates its own environment that does not interact with other python installations
- Many libraries and tools are distributed in both ecosystems.


## Check current available packages


Some python packages are working as stand-alone tools, for instance in
bioinformatics. The tool may be already installed as a module. Check if it is
there by:

```
$ module spider <tool-name or tool-name part> 
```
   
Check the pre-installed packages of a loaded python module, in shell:

```
$ pip list -v
```

To see which Python packages you, yourself, has installed, you can use `pip
list --user` while the environement you have installed the packages in are
active.

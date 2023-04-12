# Isolated environments

!!! info
    Isolated environments solve a couple of problems:

    - You can install specific, also older, versions into them.
    - You can create one for each project and no problem if the two projects require different versions.
    - You can remove the environment and create a new one, if not needed or with errors.
   
!!! question
    - How to work with isolated environments at UPPMAX?

## General procedures   

You will often have the situation that your project(s) use different versions
of Python and different versions of packages. This is great if you need
different versions of a package for different tasks, for instance. As an
example, maybe you have been using TensorFlow 1.x.x for your project and now
you need to install a package that requires TensorFlow 2.x.x but you will still
be needing the old version of TensorFlow for another package, for instance.
This is easily solved with isolated environments.

Isolated environments lets you create separate workspaces for different
versions of Python and/or different versions of packages. You can activate and
deactivate them one at a time, and work as if the other workspace does not
exist.

There are different tools for creating an isolated environement, but they all
have some things in common. At both UPPMAX is:

- You create the isolated environment with something like venv, virtualenv, or
  conda
- You activate the environment
- You install (or update) the environment with the packages you need
- You work in the isolated environment
- You deactivate the environment after use 

## Option 1: `venv`


Create a ``venv``. First load the python version you want to base your virtual
environment on:

```
$ module load python/3.6.8
$ python -m venv --system-site-packages Example
```

"Example" is the name of the virtual environment. The directory “Example” is
created in the present working directory. The ``-m`` flag makes sure that you
use the libraries from the python version you are using.

!!! note
    ``--system-site-packages`` includes the packages already installed in the loaded python module.

If you want it in a certain place like `~/test/`:

```
$ python -m venv ~/test/Example 
```

Activate it.

```
$ source <path/>Example/bin/activate
```

Note that your prompt is changing to start with (Example) to show that you are
within an environment.

Install your packages with ``pip`` and the correct versions, like:

```
pip install numpy==1.15.4 matplotlib==2.2.2
```


## Option 2: `conda`



1. First load our conda module (there is no need to install you own miniconda,
   for instance)
    ```
    module load conda
    ```
    
    * This grants you access to the latest version of Conda and all major
    repositories on all UPPMAX systems.

    * Check the text output as conda is loaded, especially the first time, see
    below

    ```
    Note thet you have a local .condarc file already
    The variable CONDA_ENVS_PATH contains the location of your environments. Set it to your project's environments folder if you have one.
    Otherwise, the default is ~/.conda/envs. Remember to export the variable with export CONDA_ENVS_PATH=/proj/...

    You may run "source conda_init.sh" to initialise your shell to be able
    to run "conda activate" and "conda deactivate" etc.
    Just remember that this command adds stuff to your shell outside the scope of the module system.

    REMEMBER TO USE 'conda clean -a' once in a while
    ```

2. If using conda for the first time
    * The variable CONDA_ENVS_PATH contains the location of your environments.
    Set it to your project's environments folder if you have one.
    * Otherwise, the default is ~/.conda/envs. 
    * Example:

    ```
    export CONDA_ENVS_PATH=/proj/snic2022-22-641/nobackup/<username>
    ```

    .. admonition:: By choice
    :class: dropdown

    Run ``source conda_init.sh`` to initialise your shell (bash) to be able
    Oto run ``conda activate`` and ``conda deactivate`` etcetera instead of
    ``source activate``. It will modify (append) your ``.bashrc`` file.

!!! info "Conda cheat sheet"
    - List packages in present environment:	``conda list``
    - List all environments:			``conda info -e`` ot ``conda env list``
    - Install a package: ``conda install somepackage``
    - Install from certain channel (conda-forge): ``conda install -c conda-forge somepackage``
    - Install a specific version: ``conda install somepackage=1.2.3``
    - Create a new environment: ``conda create --name myenvironment``
    - Create a new environment from requirements.txt: ``conda create --name myenvironment --file requirements.txt``
    - On e.g. HPC systems where you don’t have write access to central installation directory: conda create --prefix /some/path/to/env``
    - Activate a specific environment: ``conda activate myenvironment``
    - Deactivate current environment: ``conda deactivate``

3. Create the conda environment

    - Example:
    ```
    conda create --name python36-env python=3.6 numpy=1.13.1 matplotlib=2.2.2
    ```

    
    - Alternative: ``mamba`` is a fast drop-in alternative to conda, using
    "libsolv" for dependency resolution. It is available from the ``conda``
    module.
    ```
    mamba create --name python37-env python=3.7 numpy=1.13.1 matplotlib=2.2.2
    ```

4. Activate the conda environment by:
    ```
	source activate python36-env
    ```
    - You will see that your prompt is changing to start with
      ``(python-36-env)`` to show that you are within an environment.
    
5. Now do your work!

6. Deactivate
    ```
    conda deactivate
    ```

!!! warning
    - Conda is known to create **many** *small* files. Your diskspace is not only limited in GB, but also in number of files (typically ``300000`` in $home). 
    - Check your disk usage and quota limit with ``uquota``
    - Do a ``conda clean -a`` once in a while to remove unused and unnecessary files
    
    
!!! tip "Exercise 2: Create your own environment (10 min)"
    
    1. Create a virtual environment using either `venv` or `conda`. Make sure
       it's installed under `/proj/uppmax2020-2-2`
    2. Install some language technology (Python) software. 
    3. Did it work? If not what problem did you run into?

- More info about Conda on UPPMAX
  <https://uppmax.uu.se/support/user-guides/conda-user-guide/>


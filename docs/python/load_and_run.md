# Load and run python

At UPPMAX we call the applications available via the module system modules. 
    
* <https://www.uppmax.uu.se/resources/software/module-system/>

   
!!! question "Objectives"
    - Show how to load Python
    - Show how to run Python scripts and start the Python command line

!!! info "Short cheat sheet"
    - See which modules exists: ``module spider`` or ``ml spider``
    - Find module versions for a particular software: ``module spider <software>``
    - Modules depending only on what is currently loaded: ``module avail`` or ``ml av``
    - See which modules are currently loaded: ``module list`` or ``ml``
    - Load a module: ``module load <module>/<version>`` or ``ml <module>/<version>``
    - Unload a module: ``module unload <module>/<version>`` or ``ml -<module>/<version>``
    - More information about a module: ``module show <module>/<version>`` or ``ml show <module>/<version>``
    - Unload all modules except the 'sticky' modules: ``module purge`` or ``ml purge``
    

- For reproducibility reasons, you should always load a specific version of a module instead of just the default version

!!! info "Find available Python versions"

    Check all available Python versions with:

    ```
    $ module avail python
    ```

    Output at UPPMAX as of April 12 2023
    
    ```
    ---------------------------------------------------------------- /sw/mf/rackham/applications ----------------------------------------------------------------
       python_ML_packages/3.9.5-cpu    wrf-python/1.3.1

    ----------------------------------------------------------------- /sw/mf/rackham/compilers ------------------------------------------------------------------
       python/2.7.6     python/2.7.15    python/3.4.3    python/3.6.8    python/3.9.5         python3/3.6.8    python3/3.9.5
       python/2.7.9     python/3.3       python/3.5.0    python/3.7.2    python/3.10.8 (D)    python3/3.7.2    python3/3.10.8 (D)
       python/2.7.11    python/3.3.1     python/3.6.0    python/3.8.7    python3/3.6.0        python3/3.8.7

      Where:
       D:  Default Module

    Use "module spider" to find all possible modules and extensions.
    Use "module keyword key1 key2 ..." to search for all possible modules matching any of the "keys".
    ```


## Load a Python module


For reproducibility, we recommend ALWAYS loading a specific module instad of using the default version! 


Go back and check which Python modules were available. To load version 3.9.5, do:

```
module load python/3.9.5
```

!!! warning
    - Don’t use system-installed python/2.7.5
    - ALWAYS use python module

!!! info "Workflow"

    In addition to loading Python, you will also often need to load
    site-installed modules for Python packages, or use own-installed Python
    packages. The work-flow would be something like this: 


    1. Load Python and prerequisites: `module load <pre-reqs> Python/<version>``
    2. Load site-installed Python packages (optional): ``module load <pre-reqs> <python-package>/<version>``
    3. Activate your virtual environment (optional): ``source <path-to-virt-env>/bin/activate``
    4. Install any extra Python packages (optional): ``pip install --no-cache-dir --no-build-isolation <python-package>``
    5. Start Python or run python script: ``python``

    Installed Python modules (modules and own-installed) can be accessed within Python with ``import <package>`` as usual. 

    The command ``pip list`` given within Python will list the available modules to import. 

    More about packages and virtual/isolated environment to follow in later sections of the course! 


!!! tip "Keypoints"
    - Before you can run Python scripts or work in a Python shell, first load a
      python module
    - Start a Python shell session either with ``python`` or ``ipython``
    - Run scripts with ``python <script.py>``
    

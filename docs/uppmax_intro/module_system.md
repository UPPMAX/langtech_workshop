# Software and tools
!!! question "objectives"
    - We'll briefly get overviews over available software on UPPMAX

!!! info "Module system"
    - 800+ programs and packages are installed.
    - To avoid chaos and collisions, they are managed by a **module system**.
    - This system keeps installed software hidden by default, and users have to explicitly tell their terminal which version of which software they need.
    - The modules are most often available across cluster (except for Miarka)

    **Useful links**:

    - [Software at UPPMAX](https://www.uppmax.uu.se/resources/software/)
    - [Module system](https://www.uppmax.uu.se/resources/software/module-system/)

## Some commands

- list all available modules (also bio-informatics if `bioinfo-tools` is loaded)
    - `module avail` or `ml av`

- Search for modules (full name not needed and case insensitive) 
    - `module avail <part of tool name>` or `ml av <part of toolname>`

- Load a module 
    - `module load <module name>` or `ml <module name>`

- Unload a module 
    - `module unload <module name>` or `ml -<module name>`

- List loaded modules 
    - `module list` or `ml`

- Display a brief module-specific help (not available for all modules)
    - `module help <module name>` or `ml help <module name>` 
 
- Search (like `avail`) but otherwise hidden modules (`bioinfo-tools` and Easybuild modules) 
    - `module spider <part of tool name>` or `ml spider <module name>` 

## Installed software
- You can also find (almost) all installed software at:
    <https://www.uppmax.uu.se/resources/software/installed-software/>
  
## Install software yourself
- You can install in your home directory.
    - This is handy for personal needs, low numbers of files (i.e. not Conda).
- Usually better to install in project directory.
    - This way the project contains both data and software — good for reproducibility, collaboration, and everyone's general sanity.

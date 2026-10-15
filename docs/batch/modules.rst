Module System
=============

The Module system is a powerful framework that allows users to manage their software environment on
HPC systems. It provides a way to easily load and unload software packages, switch between different
versions of software, and access libraries without the need for complex configuration. For our 
purposes, we will be using software containers alongside the module system to manage software
dependencies.

After going through this module, students should be able to:

* Find software modules in the module system on TACC HPC machines
* Modify your environment by loading and unloading software modules


Tour of the Module Command
--------------------------

The module command sets the appropriate environment variable
independent of the user's shell. Typically the system will load a
default set of modules. You can list the modules loaded by:

.. code-block:: console
   
   [ls6]$ module list

   Currently Loaded Modules:
     1) intel/19.1.1   3) autotools/1.4   5) cmake/4.1.1   7) xalt/3.1
     2) impi/19.0.9    4) python3/3.9.7   6) pmix/3.2.3    8) TACC

To find out available modules for loading, a user can use:

.. code-block:: console

    [ls6]$ module avail

Press the ``<Enter>`` key to scroll through line-by-line, or the ``<Space>`` key to scroll through
page-by-page. Press ``q`` to quit the view.

If there are many modules on a system, it can be difficult to see what
modules are available to load. To display a concise listing:

.. code-block:: console

    [ls6]$ module overview

    ------------------ /opt/apps/modulefiles -----------------
     TACC    (1)   autotools     (1)   cmake    (5)   gcc   (4) 
     abaqus  (3)   biocontainers (1)   cuda     (5)   hmmer (1) 
     advisor (1)   bison         (1)   ddt      (1)   htop  (1) 

    --------- /opt/apps/intel19/impi19_0/modulefiles ---------

     Rstats (1)   amask  (2)   dealii (4)   gamess  (1)
     adcirc (1)   cp2k   (1)   fftw2  (1)   gromacs (2)
     adios2 (1)   dakota (1)   fftw3  (1)   hdf5    (1)

This shows the short name of the module (i.e. git, or biocontainers)
and the number in the parenthesis is the number of versions for each.
This list above shows that there are three versions of ``abaqus`` and one 
version of ``advisor``, for example.

To check all the versions of a package (e.g., Rstats):

.. code-block:: console

    [ls6]$ module avail Rstats

    --------------- /opt/apps/intel19/impi19_0/modulefiles ---------------
         Rstats/4.0.3

Occasionally you will see the letter ``(D)`` next to a module - that denotes it is the default
module among the different versions of that module. 
When loading packages, if you don't specify the version, the default module will be loaded. To load
packages use the commands:

.. code-block:: console

    [ls6]$ module load package1 package2 ...

To unload packages:

.. code-block:: console

    [ls6]$ module unload package1 package2 ...

Modules can also contain help messages. To access a module's help do:

.. code-block:: console

    [ls6]$ module help packageName

To get a list of all the commands that module knows about do:

.. code-block:: console

    [ls6]$ module help


EXERCISE
~~~~~~~~

Load the ``biocontainers`` module, which is a prerequisite for many other modules. After loading it,
list all available modules again to see what is new. Find a package among the biocontainers that you
have heard of before and load that, too.


Containers with Apptainer
-------------------------

Docker is not installed on TACC HPC machines. Instead, we use another containerization platform
called *Apptainer*. Importantly, Apptainer and Docker both follow the same Open Container Initiative
standard, meaning containers built one platform can be run on the other platform, and vice versa.

By default, the apptainer command is not visible, but it can be added to the environment by loading
the module.

.. code-block:: console

   [ls6]$ module spider apptainer
   ...
   [ls6]$ module load tacc-apptainer
   ...
   [ls6]$ module list
   # Double check that the apptainer command is available.


We cannot run apptainer on the login nodes, but we will revisit apptainer usage at a later point. 
But, just like with Docker, we will be using the apptainer command line interface to pull containers
from a container registry and run commands within those containers. A quick summary of the most
useful commands is as follows:

.. code-block:: console

   [ls6]$ apptainer pull <container URI>      # pull a container
   [ls6]$ apptainer shell <container.sif>     # start interactive shell in container
   [ls6]$ apptainer run <container.sif>       # run default command
   [ls6]$ apptainer exec <container.sif> CMD  # execute CMD in container environment



Review of Topics Covered
------------------------

+------------------------------------+-------------------------------------------------+
| Command                            |          Effect                                 |
+====================================+=================================================+
| ``module list``                    | List currently loaded modules                   |
+------------------------------------+-------------------------------------------------+
| ``module avail``                   | See what modules are available                  |
+------------------------------------+-------------------------------------------------+
| ``module overview``                | See what modules are available (concise)        |
+------------------------------------+-------------------------------------------------+
| ``module avail name``              | Search for module "name"                        |
+------------------------------------+-------------------------------------------------+
| ``module load name``               | Load module "name"                              |
+------------------------------------+-------------------------------------------------+
| ``module unload name``             | Unload module "name"                            |
+------------------------------------+-------------------------------------------------+
| ``module help name``               | Show module "name" help                         |
+------------------------------------+-------------------------------------------------+
| ``module help``                    | Show module command help                        |
+------------------------------------+-------------------------------------------------+


Additional Resources
--------------------

* `TACC Docs <https://docs.tacc.utexas.edu/>`_
* `Lonestar6 Docs <https://docs.tacc.utexas.edu/hpc/lonestar6/>`_
* `Lmod Docs <https://lmod.readthedocs.io/en/latest/>`_
Interactive Sessions with idev
==============================

The ``idev`` utility initiates an interactive session on one or more compute nodes
so that you can issue commands and run code as if you were doing so on your personal
machine. An interactive session is useful for development, as you can quickly compile,
run, and validate code. Accessing a single compute node is accomplished by simply
executing ``idev`` on any of the TACC systems.

Initiating an Interactive Session
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To learn about the command line options available for ``idev``, use ``idev -help``.

.. code-block:: console
   
   login1$ idev -help
   ...
   OPTION ARGUMENTS         DESCRIPTION
   -A     account_name      sets account name (default: in .idevrc)
   -m     minutes           sets time in minutes (default: 30)
   -p     queue_name        sets queue to named queue (default: -p development)
   -r     resource_name     sets hardware
   -t     hh:mm:ss          sets time to hh:mm:ss (default: 00:30:00)
   -help      [--help     ] displays (this) help message
   -v         [--version  ] output version information and exit

Let's go over some of the most useful ``idev`` command line options that can customize your interactive session:

To change the **time** limit to be lesser or greater than the default 30 minutes, users can use the ``-m`` command line option. For example, a user requesting an interactive session for an hour would use the command line option ``-m 60``.

To change the **account_name** associated with the interactive session, users can use the ``-A`` command line option. This option is useful for when a user has multiple allocations they belong to. For example, if I have allocations on accounts ``TACC`` and ``Training``, I can use ``-A`` to set the allocation I want to be used like so: ``-A TACC`` or ``-A Training``.

To change the **queue** to be different than the default ``development`` queue, users can use the ``-p`` command line option. For example, if a user wants to launch an interactive session on one of Lonestar6's GPU nodes, they would use the command line option ``-p gpu-a100`` or ``-p gpu-a100-dev``. You can learn more about the different queues of Lonestar6 `here <https://docs.tacc.utexas.edu/hpc/lonestar6/#table5>`_.

Note: For the scope of this section, we will be using the default ``development`` queue.  

To start a thirty-minute interactive session on a compute node in the development queue with our ``EXAMPLE`` allocation:

.. code-block:: console
   
   login1$ idev -A EXAMPLE   

If launch is successful, you will see output that includes the following excerpts:

.. code-block:: console
   
   ...
   -----------------------------------------------------------------
         Welcome to the Lonestar6 Supercomputer          
   -----------------------------------------------------------------
   ...

   -> After your idev job begins to run, a command prompt will appear,
   -> and you can begin your interactive development session. 
   -> We will report the job status every 4 seconds: (PD=pending, R=running).

   -> job status:  PD
   -> job status:  R

   -> Job is now running on masternode= c449-0015...OK
   ...
   c449-0015(268)$

Exercise
^^^^^^^^

Let's revisit the job we ran in the previous section. This time, we will be going through each command we entered into ``job.slurm`` interactively.

.. code-block:: console

   c449-0015(268)$ pwd
   /home1/03439/wallen/IntroToLinuxHPC/Lab04
   c449-0015(269)$ ls
   data job.slurm results vina_job.o864828

.. code-block:: console

   c449-0015(270)$ echo "starting at:"
   starting at:
   c449-0015(271)$ date
   Mon Jun 29 0X:XX:XX CDT 2020
   c449-0015(272)$ module list

   Currently Loaded Modules:
   #  it is okay if you have loaded modules from past sessions

   c449-0015(273)$ module use /work/03439/wallen/public/modulefiles
   c449-0115(275)$ module load autodock_vina/1.2.3
   c449-0115(276)$ module list

   Currently Loaded Modules:
   1) intel/17.0.4 
   2) boost/1.64
   3) autodock_vina/1.1.2     #the order in which the modules are listed does not matter

   c449-0015(277)$ cd data/
   c449-0015(278)$ vina --config configuration_file.txt --out ../results/output_ligands.pdbqt 
   #################################################################
   # If you used AutoDock Vina in your work, please cite:          #
   #                                                               #
   # O. Trott, A. J. Olson,                                        #
   # AutoDock Vina: improving the speed and accuracy of docking    #
   # with a new scoring function, efficient optimization and       #
   # multithreading, Journal of Computational Chemistry 31 (2010)  #
   # 455-461                                                       #
   #                                                               #
   # DOI 10.1002/jcc.21334                                         #
   #                                                               #
   # Please see http://vina.scripps.edu for more information.      #
   #################################################################

   Detected 272 CPUs
   WARNING: at low exhaustiveness, it may be impossible to utilize all CPUs
   Reading input ... done.
   Setting up the scoring function ... done.
   Analyzing the binding site ... done.
   Using random seed: -31156704
   Performing search ... 
   0%   10   20   30   40   50   60   70   80   90   100%
   |----|----|----|----|----|----|----|----|----|----|
   ***************************************************
   done.
   Refining results ... done.

   mode |   affinity | dist from best mode
        | (kcal/mol) | rmsd l.b.| rmsd u.b.
   -----+------------+----------+----------
      1        -12.3      0.000      0.000
      2        -11.1      1.223      1.866
      3        -11.0      3.000     12.459
      4        -10.5      2.268     12.434
      5        -10.4      2.272     13.237
      6        -10.3      3.146     13.666
      7        -10.3      3.553     12.345
      8        -10.2      1.827     13.667
      9         -9.8      2.608     12.630
   Writing output ... done.

   c449-0015(279)$ echo "ending at:"
   c449-0015(280)$ date
   Mon Jun 29 0X:XX:XX CDT 2020

To exit an interactive session, you can use the command ``logout``.
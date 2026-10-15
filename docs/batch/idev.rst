Interactive Sessions with idev
==============================

The ``idev`` utility initiates an interactive session on one or more compute nodes
so that you can issue commands and run code as if you were doing so on your personal
machine. An interactive session is useful for development, as you can quickly compile,
run, and validate code. Accessing a single compute node is accomplished by simply
executing ``idev`` on any of the TACC systems. After going through this module, students
should be able to:

* Use the ``idev`` utility to launch an interactive session on a compute node
* Customize the interactive session using command line options

Initiating an Interactive Session
---------------------------------

To learn about the command line options available for ``idev``, use ``idev --help``.

.. code-block:: console
   
   [ls6]$ idev --help
                                                                                                             
      Usage:  idev [OPTIONS]

      idev creates an Interactive session on a compute node for
      DEVelopment: compiling, and executing serial, openmp-parallel,
      or mpi-parallel code as you would in a batch job.
      Supported systems: frontera, ls6, stampede3, vista.

      Idev, by default,  uses a single node and charges the project stored in $HOME/.idevrc.
      Options can be in any order.

      OPTION   ARGUMENTS          DESCRIPTION

        -A     account_name       sets account name (default:  TACC-SCI)
        -m     minutes            sets time in minutes (default: 30)
        -n     total_tasks        Total number of tasks
        -N     nodes              Number of nodes
        -tpn   tpn                Tasks per node
                                  -tasks-per-node|--tasks-per-node   tpn  (-tpn alternate)
                                  -ntasks-per-node|--ntasks-per-node tpn  (-tpn alternate)
        -p     partition_name     sets queue to partition name (default: development)
        -R                        Finds a reservation for the user.
        -r     reservation_name   requests use of a specific reservation
        ...



Some of the most useful flags to customize the session include:

* To change the **time** limit to something other than the default 30 minutes, 
  use the ``-m`` command line option. For example, requesting an interactive session for an
  hour would use the command line option ``-m 60``.
* To change the **queue** to something other than the default ``development`` queue, use the 
  ``-p`` command line option. For example, to launch an interactive session on one of 
  Lonestar6's GPU nodes, use the command line option ``-p gpu-a100`` or ``-p gpu-a100-dev``. 
  You can learn more about the different queues of Lonestar6 `here <https://docs.tacc.utexas.edu/hpc/lonestar6/#table5>`_.
* To start a two-hour interactive session on a compute node in the development queue with 
  our ``OTH24028`` allocation:

.. code-block:: console
   
   [ls6]$ idev -m 120 -p development -A OTH24028

If successful, you will see output that includes the following excerpts:

.. code-block:: console
      
    -> NOTE: "->" are idev statements. "-->" are TACC/SLURM filter statements.                                                                                                                                         
    -> NO RESERVATIONS  found for wallen.                                                                    
    -> Checking on the status of development queue. OK                                                       
   
    -> Defaults file    : ~/.idevrc                                                                          
    -> System           : ls6                                                                                                                                                                                          
    -> Queue            : development    (idev  default queue )                                                                                                                                                        
    -> Nodes            : 1              (idev  default       )                                                                                                                                                        
    -> Tasks per Node   : 128            (Queue default       )                                                                                                                                                        
    -> Time (minutes)   : 120            (cmd line: -m        )                                                                                                                                                        
    -> Project          : OTH24028       (~/.idevrc           )                                                                                                                                                        
                                                        
   -----------------------------------------------------------------                                                                                                                                                   
              Welcome to the Lonestar6 Supercomputer                                                                                                                                                                   
   -----------------------------------------------------------------                                                                                                                                                   
                                                                                                             
   No reservation for this job                                                                                                                                                                                         
   --> Verifying valid submit host (staff)...OK                                                              
   --> Verifying valid jobname...OK                                                                                                                                                                                    
   --> Verifying valid ssh keys...OK                                                                         
   --> Verifying access to desired queue (development)...OK                                                                                                                                                            
   --> Checking available allocation (OTH24028)...OK                                                         
   --> Verifying that quota for filesystem /home1/03439/wallen is at 75.08% allocated...OK                                                                                                                             
   --> Verifying that quota for filesystem /work/03439/wallen/ls6 is at 62.13% allocated...OK                                                                                                                          
   Submitted batch job 3085466                                                                               
   ...
   c307-006.ls6(1000)$ 

Ultimately the command prompt will change from a login node to a compute node, and you will be able 
to run commands directly as if you were on your local machine.

EXERCISE
~~~~~~~~

Let's revisit the job we ran in the previous section. This time, we will be going through each
command we entered into ``job.slurm`` interactively.

.. code-block:: console

   c449-0015(268)$ pwd
   /work/03439/wallen/ls6/docking-example/
   c449-0015(269)$ ls
   configuration_file.txt*  docking-ex.o3083211  ligand.pdbqt*         protein.pdbqt*
   docking-ex.e3083211      job.slurm            output_ligands.pdbqt*

.. code-block:: console

   c449-0015(270)$ echo "starting at:"
   starting at:
   c449-0015(271)$ date
   Tue Apr 14 12:25:39 CDT 2026
   c449-0015(272)$ module list

   Currently Loaded Modules:
   1) intel/19.1.1    4) python3/3.9.7   7) xalt/3.1            
   2) impi/19.0.9     5) cmake/4.1.1     8) TACC                
   3) autotools/1.4   6) pmix/3.2.3      9) tacc-apptainer/1.1.8

   c449-0015(273)$ module use /work/03439/wallen/public/modulefiles
   c449-0115(275)$ module load autodock_vina/1.2.3
   c449-0115(276)$ module list

   Currently Loaded Modules:
   1) intel/19.1.1    5) pmix/3.2.3             9) python3/3.9.7      
   2) impi/19.0.9     6) xalt/3.1              10) autodock_vina/1.2.3
   3) autotools/1.4   7) TACC                                         
   4) cmake/4.1.1     8) tacc-apptainer/1.1.8                         

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
   Tue Apr 14 12:25:56 CDT 2026

To exit an interactive session, you can use the command ``logout``.


EXERCISE
~~~~~~~~

1. Unload the autodock_vina module (if currently loaded).
2. Load the tacc-apptainer module and the biocontainers module.
3. Search for and load an autodock_vina container module, or find and pull an autodock_vina
   container from DockerHub.
4. Run the above vina command again using the containerized version of vina.



Additional Resources
--------------------

* `TACC Docs <https://docs.tacc.utexas.edu/>`_
* `Lonestar6 Docs <https://docs.tacc.utexas.edu/hpc/lonestar6/>`_
* `AutoDock-Vina <https://github.com/ccsb-scripps/AutoDock-Vina>`_

Creating and Manipulating Files
===============================

We have seen how to navigate around the filesystem and perform operations with folders. But, what about files? Just like on Windows or Mac, we can easily create new files, copy files, rename files, and move files to different locations. First, we will navigate to the home directory and create a few new folders and files with the ``mkdir`` and ``touch`` commands:

.. code-block:: console

   $ cd     # cd on an empty line will automatically take you back to the home directory
   $ pwd
   /home1/03439/wallen
   $ mkdir folder1
   $ mkdir folder2
   $ mkdir folder3
   $ touch file_a
   $ touch file_b
   $ touch file_c
   $ ls
   file_a  file_b  file_c  folder1  folder2  folder3

These files we have created are all empty. Removing a file is done with the ``rm`` (remove) command. Please note that on Linux file systems, there is no "Recycle Bin". Any file or folder removed is gone forever and often un-recoverable:

.. code-block:: console 

   $ touch junkfile
   $ rm junkfile

Moving files with the ``mv`` command and copying files with the ``cp`` command works similarly to how you would expect on a Windows or Mac machine. The context around the move or copy operation determines what the result will be. For example, we could move and/or copy files into folders:

.. code-block:: console

   $ mv file_a folder1/
   $ mv file_b folder2/
   $ cp file_c folder3/

Before listing the results with ``ls`` or ``tree``, try to guess what the result will be.

.. code-block:: console

   $ tree .
   .
   |-- file_c
   |-- folder1
   |   `-- file_a
   |-- folder2
   |   `-- file_b
   `-- folder3
       `-- file_c

Two files have been moved into folders, and ``file_c`` has been copied - so there is still a copy of ``file_c`` in the home directory. Move and copy commands can also be used to change the name of a file:

.. code-block:: console

   $ cp file_c file_c_copy
   $ mv file_c file_c_new_name

By now, you may have found that Linux is very unforgiving with typos. Generous use of the ``<Tab>`` key to auto-complete file and folder names, as well as the ``<UpArrow>`` to cycle back through command history, will greatly improve the experience. As a general rule, try not to use spaces or strange characters in files or folder names. Stick to:

.. code-block:: console

   A-Z     # capital letters
   a-z     # lowercase letters
   0-9     # digits
   -       # hyphen
   _       # underscore
   .       # period

Before we move on, let's clean up once again by removing the files and folders we have created. Do you remember the command for removing non-empty folders?

.. code-block:: console

   $ rm -r folder1
   $ rm -r folder2
   $ rm -r folder3

How do we remove ``file_c_copy`` and ``file_c_new_name``?

.. code-block:: console

   $ rm file_c_copy
   $ rm file_c_new_name


Review of Topics Covered
^^^^^^^^^^^^^^^^^^^^^^^^

+------------------------------------+-------------------------------------------------+
| Command                            |          Effect                                 |
+====================================+=================================================+
| ``touch file_name``                |  create a new file                              |
+------------------------------------+-------------------------------------------------+
| ``rm file_name``                   |  remove a file                                  |
+------------------------------------+-------------------------------------------------+
| ``rm -r dir_name/``                |  remove a directory and its contents            |                                                 
+------------------------------------+-------------------------------------------------+
| ``mv file_name dir_name/``         |  move a file into a directory                   |
+------------------------------------+-------------------------------------------------+
| ``mv old_file new_file``           |  change the name of a file                      |
+------------------------------------+-------------------------------------------------+
| ``mv old_dir/ new_dir/``           |  change the name of a directory                 |
+------------------------------------+-------------------------------------------------+
| ``cp old_file new_file``           |  copy a file                                    |
+------------------------------------+-------------------------------------------------+
| ``cp -r old_dir/ new_dir/``        |  copy a directory                               |
+------------------------------------+-------------------------------------------------+
| ``<Tab>``                          |  autocomplete file or folder names              |
+------------------------------------+-------------------------------------------------+
| ``<UpArrow>``                      |  cycle through command history                  |
+------------------------------------+-------------------------------------------------+

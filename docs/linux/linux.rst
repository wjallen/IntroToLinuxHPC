Linux Command Line 
==================

Modern computational research is conducted primarily on Linux-based systems. Most research computing
infrastructure, including the HPC clusters and cloud resources at TACC, runs Linux and supports
software developed for Linux environments. These systems are accessed through a **command-line
interface (CLI)**, a text-based interface where users type commands to interact directly with a
computer. In research computing, the CLI is used to log into remote systems, manage files, and
launch computational analyses.

Learning how to use the Linux command line interface is therefore an essential skill for research
computing. Once you are comfortable working in a Linux environment, you can work on virtually any
research computing system in the world. After completing this module, participants should be able to:

 * Describe basic functions of essential Linux commands
 * Use Linux commands to navigate a file system and manipulate files
 * Edit files directly on a Linux system using a command line utility (e.g. vim, nano, emacs)
 * Transfer data to a remote Linux file system
 * Print, identify, and modify environment variables

Topics covered include:

 * Creating and changing folders (``pwd``, ``ls``, ``mkdir``, ``cd``, ``rmdir``)
 * Creating and manipulating files (``touch``, ``rm``, ``mv``, ``cp``)
 * Looking at the Contents of files (``cat``, ``more``, ``less``, ``head``, ``tail``, ``grep``)
 * Network and file transfers (``hostname``, ``whoami``, ``logout``, ``ssh``, ``scp``, ``rsync``)




Creating and Changing Folders
-----------------------------

On a Windows or Mac desktop, our present location determines what files and folders
we can access. I can "see" my present location visually with the help of the graphic
interface - I could be looking at my Desktop, or the contents of a folder, for example.
In a Linux command-line interface, we lack the same visual queues to tell us what our
location is. Instead, we use a command - ``pwd`` (print working directory) - to tell
us our present location. Try executing this command on Lonestar6:

.. code-block:: console

   $ pwd
   /home1/03439/wallen

This home location on the Linux filesystem is unique for each user, and it is roughly
analogous to C:\\Users\\username on Windows, or /Users/username on Mac.

To see what files and folders are available at this location, use the ``ls`` (list) command:

.. code-block:: console

   $ ls

I have no files or folders in my home directory yet, so I do not get a response.
We can create some folders using the ``mkdir`` (make directory) command. The words 
'folder' and 'directory' are interchangeable:

.. code-block:: console

   $ mkdir folder1
   $ mkdir folder2
   $ mkdir folder3

.. code-block:: console

   $ ls
   folder1 folder2 folder3

Now we have some folders to work with. To "open" a folder, navigate into that folder 
using the ``cd`` (change directory) command. This process is analogous to double-clicking 
a folder on Windows or Mac:

.. code-block:: console

   $ pwd
   /home/03439/wallen/
   $ cd folder1
   $ pwd
   /home1/03439/wallen/folder1

Now that we are inside ``folder1``, make a few sub-folders:

.. code-block:: console

   $ mkdir subfolderA
   $ mkdir subfolderB
   $ mkdir subfolderC
   $ ls
   subfolderA subfolderB subfolderC

Use ``cd`` to Navigate into ``subfolderA``, then use ``ls`` to list the contents. What do you expect to see?

.. code-block:: console

   $ cd subfolderA
   $ pwd  
   /home/03439/wallen/folder1/subfolderA
   $ ls

There is nothing there because we have not made anything yet. Next, we will navigate back to the 
home directory. So far we have seen how to navigate "down" into folders, but how do we navigate 
back "up" to the parent folder? There are different ways to do it. For example, we could specify 
the complete path of where we want to go:

.. code-block:: console

   $ pwd
   /home1/03439/wallen/folder1/subfolderA
   $ cd /home1/03439/wallen/folder1
   $ pwd
   /home1/03439/wallen/folder1/

Or, we could use a shortcut, ``..``, which refers to the **parent folder** - one level higher 
than the present location:

.. code-block:: console

   $ pwd
   /home1/03439/wallen/folder1
   $ cd ..
   $ pwd
   /home1/03439/wallen

We are back in our home directory. Finally, use the  ``rmdir`` (remove directory) command to remove 
folders. This will not work on folders that have any contents (more on this later):

.. code-block:: console

   $ mkdir junkfolder
   $ ls
   folder1 folder2 folder3 junkfolder
   $ rmdir junkfolder
   $ ls
   folder1 folder2 folder3

A bonus command available on some Linux operating systems is called ``tree``. The ``tree`` command 
displays files and folders in a hierarchical view. Use another Linux shortcut, ``.``, to indicate 
that you want to list files and folders in your **present location**.

.. code-block:: console

   $ tree .
   .
   |-- folder1
   |   |-- subfolderA
   |   |-- subfolderB
   |   `-- subfolderC
   |-- folder2
   `-- folder3

Before we move on, let's remove the directories we have made, using ``rm -r`` to remove our parent 
folder ``folder1`` and its subfolders. The ``-r`` command line option recursively removes subfolders 
and files located "down" the parent directory. ``-r`` is required for non-empty folders.

.. code-block:: console

   $ rm -r folder1
   $ ls 
   folder2 folder3

Which command should we use to remove ``folder2`` and ``folder3``?

.. code-block:: console

   $ rmdir folder2
   $ rmdir folder3
   $ ls

Why could we use ``rmdir`` on ``folder2`` and ``folder3``, but not on ``folder1``?





Creating and Manipulating Files
-------------------------------

We have seen how to navigate around the filesystem and perform operations with folders. But, what
about files? Just like on Windows or Mac, we can easily create new files, copy files, rename files,
and move files to different locations. First, we will navigate to the home directory and create a
few new folders and files with the ``mkdir`` and ``touch`` commands:

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

These files we have created are all empty. Removing a file is done with the ``rm`` (remove) command.
Please note that on Linux file systems, there is no "Recycle Bin". Any file or folder removed is
gone forever and often un-recoverable:

.. code-block:: console 

   $ touch junkfile
   $ rm junkfile

Moving files with the ``mv`` command and copying files with the ``cp`` command works similarly to
how you would expect on a Windows or Mac machine. The context around the move or copy operation
determines what the result will be. For example, we could move and/or copy files into folders:

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

Two files have been moved into folders, and ``file_c`` has been copied - so there is still a copy
of ``file_c`` in the home directory. Move and copy commands can also be used to change the name of
a file:

.. code-block:: console

   $ cp file_c file_c_copy
   $ mv file_c file_c_new_name

By now, you may have found that Linux is very unforgiving with typos. Generous use of the ``<Tab>``
key to auto-complete file and folder names, as well as the ``<UpArrow>`` to cycle back through
command history, will greatly improve the experience. As a general rule, try not to use spaces or
strange characters in files or folder names. Stick to:

.. code-block:: console

   A-Z     # capital letters
   a-z     # lowercase letters
   0-9     # digits
   -       # hyphen
   _       # underscore
   .       # period

Before we move on, let's clean up once again by removing the files and folders we have created. Do
you remember the command for removing non-empty folders?

.. code-block:: console

   $ rm -r folder1
   $ rm -r folder2
   $ rm -r folder3

How do we remove ``file_c_copy`` and ``file_c_new_name``?

.. code-block:: console

   $ rm file_c_copy
   $ rm file_c_new_name




Looking at the Contents of Files
--------------------------------

Everything we have seen so far has been with empty files and folders. We will now start looking at
some real data. Navigate to your home directory, then issue the following ``cp`` command to copy a
"tar archive" file from me:

.. code-block:: console

   $ cd ~    # the tilde ~ is also a shortcut referring to your home directory
   $ pwd
   /home1/03439/wallen
   $ cp /work/03439/wallen/public/IntroToLinuxHPC.tar .

Try to use ``<Tab>`` to autocomplete the name of the file. Do NOT change the username or lustre
number to your username and lustre number - in this case you are copying a file from my directory
to your directory. Also, please notice the single dot ``.`` at the end of the copy command, which
indicates that you want to cp the tar archive to ``.``, this present location (your home directory).

This archive file is actually a bundle of many files and folders, all packed into one nice, easily
transportable object. Once it is copied over, un-pack the file with the following command:

.. code-block:: console

   $ ls
   IntroToLinuxHPC.tar
   $ tar -xvf IntroToLinuxHPC.tar

In the first lab (``Lab01``), we have a file called ``websters.txt``. This a list of all the words
in Webster's Dictionary. But how can we see the contents of the file?

.. code-block:: console

   $ cd IntroToLinuxHPC
   $ cd Lab01
   $ pwd
   /home1/03439/wallen/IntroToLinuxHPC/Lab01
   $ ls
   README websters.txt

If you want to see the contents of a file, use the ``cat`` command to print it to screen:

.. code-block:: console

   $ cat websters.txt
   A
   a
   aa
   aal
   aalii
   aam
   Aani
   aardvark

This is a long file! Printing everything to screen is much too fast and not very useful. We can use
a few other commands to look at the contents of the file with ``more`` control:

.. code-block:: console

   $ more websters.txt

Press the ``<Enter>`` key to scroll through line-by-line, or the ``<Space>`` key to scroll through
page-by-page. Press ``q`` to quit the view, or ``<Ctrl+c>`` to force a quit if things freeze up. A
``%`` indicator at the bottom of the screen shows your progress through the file. This is still a
little bit messy and fills up the screen. The ``less`` command has the same effect, but is a little
bit cleaner:

.. code-block:: console

   $ less websters.txt

Scrolling through the data is the same, but now we can also search the data. Press the ``/`` forward
slash key, and type a word that you would like to search for. The screen will jump down to the first
match of that word. The ``n`` key will cycle through other matches, if they exist.

Finally, you can view just the beginning or the end of a file with the ``head`` and ``tail``
commands. For example:

.. code-block:: console

   $ head websters.txt
   $ tail websters.txt

The ``>`` and ``>>`` shortcuts in Linux indicate that you would like to redirect the output of one
of the commands above. Instead of printing to screen, the output can be redirected into a file:

.. code-block:: console

   $ cat websters.txt > websters_new.txt
   $ head websters.txt > first_10_lines.txt

A single greater than sign ``>`` will redirect and **overwrite** any contents in the target file. A
double greater than sign ``>>`` will redirect and **append** any output to the end of the target
file.

One final useful way to look at the contents of files is with the ``grep`` command. ``grep``
searches a file for a specific pattern, and returns all lines that match the pattern. For example:

.. code-block:: console

   $ grep "banana" websters.txt
   banana
   cassabanana

Although it is not always necessary, it is safe to put the search term in quotes. More on ``grep`` later.

EXERCISE
~~~~~~~~

1. Extract every word from ``websters.txt`` that contains the string ``apple``, and put it into a new file called ``apple.txt``.
2. Extract every word from ``websters.txt`` that contains the string ``carrot``, and put it into a new file called ``carrot.txt``.
3. Extract every word from ``websters.txt`` that contains the string ``cheese``, and put it into a new file called ``cheese.txt``.
4. Examine the contents of ``apple.txt``, ``carrot.txt``, and ``cheese.txt`` to make sure they contain what you expect.
5. Concatenate all three lists into a new file called ``food.txt``.




Network and File Transfers
--------------------------

In order to login or transfer files to a remote Linux file system, you must know the hostname
(unique network identifier) and the username. If you are already on a Linux file system, those are
easy to determine using the following commands:

.. code-block:: console

   $ whoami
   wallen
   $ hostname -f
   login4.ls6.tacc.utexas.edu

Given that information, a user would remotely login to this Linux machine using the Terminal
command:

.. code-block:: console

   $ ssh wallen@ls6.tacc.utexas.edu
   (enter password)
   (enter token)

Windows users would typically use the program **PuTTY** to perform this operation. Logging out of a
remote system is done using the ``logout`` command, or the shortcut ``<Ctrl+d>``:

.. code-block:: console

  [ls6]$ logout
  [local]$

To practice transferring files to Lonestar6's ``$WORK`` and ``$SCRATCH``, we need to identify the
path to our ``$WORK`` and ``$SCRATCH`` directory. To identify these paths, we can use helpful command shortcuts.

To identify the path to our ``$WORK`` directory, we can use ``cd $WORK`` or the helpful shortcut
``cdw``:

.. code-block:: console
   
   $ cdw
   $ pwd
   /work/03439/wallen/ls6

To identify the path to our ``$SCRATCH`` directory, we can use ``cd $SCRATCH`` or the helpful
shortcut ``cds``:

.. code-block:: console
   
   $ cds
   $ pwd
   /scratch/03439/wallen    

Copying files from your local computer to Lonestar6's ``$WORK`` would require the ``scp`` command
(Windows users use the program "WinSCP"):

.. code-block:: console

   [local]$ scp my_file wallen@ls6.tacc.utexas.edu:/work/03439/wallen/ls6
   (enter password)
   (enter token)

In this command, you specify the name of the file you want to transfer (``my_file``), the username
(``wallen``), the hostname (``ls6.tacc.utexas.edu``), and the path you want to put the file
(``/work/03439/wallen/ls6``). Take careful notice of the separators including spaces, the @ symbol,
and the colon. 

Copying files from your local computer to Lonestar6's ``$SCRATCH`` using ``scp``:

.. code-block:: console

   [local]$ scp my_file wallen@ls6.tacc.utexas.edu:/scratch/03439/wallen
   (enter password)
   (enter token)

Copy files from Lonestar6 to your local computer using the following:

.. code-block:: console

   [local]$ scp wallen@ls6.tacc.utexas.edu:/work/03439/wallen/ls6/my_file ./
   (enter password)
   (enter token)

Note: If you wanted to copy ``my_file`` from ``$SCRATCH``, the path you would specify after the
colon would be ``/scratch/03439/wallen/my_file``.
 
Instead of files, full directories can be copied using the "recursive" flag (``scp -r ...``). The
``rsync`` tool is an advanced copy tool that is useful for synching data between two sites. Although
we will not go into depth here, example ``rsync`` usage is as follows:

.. code-block:: console

   $ rsync -azv local remote
   $ rsync -azv remote local

This is just the basics of copying files. See example ``scp`` usage
`here-1 <https://en.wikipedia.org/wiki/Secure_copy>`_ and example ``rsync`` usage
`here-2 <https://en.wikipedia.org/wiki/Rsync>`_.


EXERCISE
~~~~~~~~

1. Identify which Lonestar6 login node you are on (login1, login2, login3)
2. Remotely login to a different Lonestar6 login node and list what files are available.
3. Logout until you are back to your original login node.
4. Make your own ``my_file`` on your local computer using knowledge from our previous sections and copy ``my_file`` to your ``$WORK`` file system on Lonestar6 









Review of Topics Covered
------------------------

+------------------------------------+-------------------------------------------------+
| Command                            |          Effect                                 |
+====================================+=================================================+
| ``pwd``                            |  print working directory                        |
+------------------------------------+-------------------------------------------------+
| ``ls``                             |  list files and directories                     |
+------------------------------------+-------------------------------------------------+
| ``ls -l``                          |  list files in column format                    |                                                 
+------------------------------------+-------------------------------------------------+
| ``mkdir dir_name/``                |  make a new directory                           |
+------------------------------------+-------------------------------------------------+
| ``cd dir_name/``                   |  navigate into a directory                      |
+------------------------------------+-------------------------------------------------+
| ``rmdir dir_name/``                |  remove an empty directory                      |
+------------------------------------+-------------------------------------------------+
| ``rm -r dir_name/``                |  remove a directory and its contents            |
+------------------------------------+-------------------------------------------------+
| ``tree``                           |  list files and directories hierarchically      |
+------------------------------------+-------------------------------------------------+
| ``.`` or ``./``                    |  refers to the present location                 |
+------------------------------------+-------------------------------------------------+
| ``..`` or ``../``                  |  refers to the parent directory                 |
+------------------------------------+-------------------------------------------------+




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




+------------------------------------+-------------------------------------------------+
| Command                            |          Effect                                 |
+====================================+=================================================+
| ``cat file_name``                  |  print file contents to screen                  |
+------------------------------------+-------------------------------------------------+
| ``cat file_name >> new_file``      |  redirect output to new file                    |
+------------------------------------+-------------------------------------------------+
| ``more file_name``                 |  scroll through file contents                   |                                                 
+------------------------------------+-------------------------------------------------+
| ``less file_name``                 |  scroll through file contents                   |
+------------------------------------+-------------------------------------------------+
| ``head file_name``                 |  output beginning of file                       |
+------------------------------------+-------------------------------------------------+
| ``tail file_name``                 |  output end of a file                           |
+------------------------------------+-------------------------------------------------+
|  ``grep pattern file_name``        |  search for 'pattern' in a file                 |
+------------------------------------+-------------------------------------------------+
|  ``~/``                            |  shortcut for home directory                    |
+------------------------------------+-------------------------------------------------+
|  ``<Ctrl+c>``                      |  force interrupt                                |
+------------------------------------+-------------------------------------------------+
|  ``>``                             |  redirect and overwrite                         |
+------------------------------------+-------------------------------------------------+
|  ``>>``                            |  redirect and append                            |
+------------------------------------+-------------------------------------------------+




+------------------------------------+-------------------------------------------------+
| Command                            |          Effect                                 |
+====================================+=================================================+
| ``hostname -f``                    |  print hostname                                 |
+------------------------------------+-------------------------------------------------+
| ``whoami``                         |  print username                                 |
+------------------------------------+-------------------------------------------------+
| ``ssh username@hostname``          |  remote login                                   |                                                 
+------------------------------------+-------------------------------------------------+
| ``logout``                         |  logout                                         |
+------------------------------------+-------------------------------------------------+
| ``cd $WORK``, ``cdw``              |  navigate to ``$WORK`` file system              |
+------------------------------------+-------------------------------------------------+
| ``cd $SCRATCH``, ``cds``           |  navigate to ``$SCRATCH`` file system           |
+------------------------------------+-------------------------------------------------+
| ``scp local remote``               |  copy a file from local to remote               |
+------------------------------------+-------------------------------------------------+
| ``scp remote local``               |  copy a file from remote to local               |
+------------------------------------+-------------------------------------------------+
|  ``rsync -azv local remote``       |  sync files between local and remote            |
+------------------------------------+-------------------------------------------------+
|  ``rsync -azv remote local``       |  sync files between remote and local            |
+------------------------------------+-------------------------------------------------+
|  ``<Ctrl+d>``                      |  logout of host                                 |
+------------------------------------+-------------------------------------------------+






Additional Resources
--------------------

* `Practice Linux commands safely in a web-based emulator <https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192>`_
* `This is a good summary of the important commands you need to know <https://linuxjourney.com/lesson/the-shell>`_


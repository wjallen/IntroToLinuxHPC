
Getting Set Up
==============

To log in to Lonestar6, follow the instructions for your operating system below.

Mac / Linux
^^^^^^^^^^^
.. code-block:: console

   Open the application 'Terminal'
   ssh username@ls6.tacc.utexas.edu
   (enter password)
   (enter 6-digit token)

Windows
^^^^^^^

Windows users will need to install an SSH client like **PuTTY** to follow along. If you
have not done so already, download the **PuTTY** "Windows Installer"
`here <https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html>`_. (Other tools like
PowerShell work, too).

Once **PuTTY** is installed:

* Double-click the **PuTTY** icon
* In the **PuTTY** Configuration window make sure the Connection type is SSH
* enter ``ls6.tacc.utexas.edu`` for Host Name
* click "Open"
* answer "Yes" to the SSH security question

In the **PuTTY** terminal:

* enter your TACC user id after the "login as:" prompt, then Enter
* enter the password associated with your TACC account
* enter your 6-digit TACC token value

.. code-block:: console

   Open the application 'PuTTY'
   enter Host Name: ls6.tacc.utexas.edu
   (click 'Open')
   (enter username)
   (enter password)
   (enter 6-digit token)

Successful Login to Lonestar6
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If your login was successful, your terminal will look something like this:


.. code-block:: console 

  ------------------------------------------------------------------------------
   Welcome to the Lonestar6 Supercomputer
   Texas Advanced Computing Center, The University of Texas at Austin
   ------------------------------------------------------------------------------
   
   Unauthorized use/access is prohibited. **
   If you log on to this computer system, you acknowledge your awareness
   of and concurrence with the UT Austin Acceptable Use Policy. The
   University will prosecute violators to the full extent of the law.
   
   TACC Usage Policies:
   http://www.tacc.utexas.edu/user-services/usage-policies/
   ______________________________________________________________________
   
   Welcome to Lonestar6, please read these important system notes:
   
   --> Lonestar6 user documentation is available at:
   https://portal.tacc.utexas.edu/user-guides/lonestar6
   
   ---------------------- Project balances for user wallen -----------------------
   | Name           Avail SUs     Expires | Name           Avail SUs     Expires |
   | DBS22003             500  2024-09-30 | DrugDiscovery       4171  2024-03-31 | 
   | TACC-SCI           46050  2025-06-30 | OTH22024           17388  2024-06-30 | 
   | IBN22007            1954  2024-09-30 |                                      |
   ------------------------- Disk quotas for user wallen -------------------------
   | Disk         Usage (GB)     Limit    %Used   File Usage       Limit   %Used |
   | /scratch          238.1       0.0     0.00        61321           0    0.00 |
   | /home1              3.6      11.7    30.37        18502           0    0.00 |
   | /work             453.8    1024.0    44.31      2120925     3000000   70.70 |
   -------------------------------------------------------------------------------
   
   Tip 184   (See "module help tacc_tips" for features or how to disable)
   
      Emacs allows users to enter UTF-8 character with the sequence C-x 8 ... For example, C-x 8 ~ n produces ?. C-x 8 RET
      followed by either the code point in hex or the name of the official Unicode name of the character.


A Note About Quotas
^^^^^^^^^^^^^^^^^^^

The welcome message you receive upon successful login to Lonestar6 has useful information
for you to keep track of. Especially of note is the breakdown of disk quotas for your account,
as you can keep an eye on whether your usage is nearing the determined limit. 

Once your usage is nearing the quota, you'll start to experience issues that will not only
impact your own work, but also impact the system for others. For example, if you're nearing
your quota in ``$WORK``, and your job is repeatedly trying (and failing) to write to ``$WORK``,
you will stress that file system.

Another useful way to monitor your disk quotas (and TACC project balances) at any time is to execute:

.. code-block:: console

   [ls6]$ /usr/local/etc/taccinfo



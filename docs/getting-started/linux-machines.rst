.. _linux-machines:

=====================
Linux Workstations
=====================
| Contributors: Nathan TM Huneke, Harry Fagan, Nick Hedger, Yukai Zou
| Maintainers: Nathan TM Huneke

--------------

Why Linux?
-------------

Linux is a lightweight (small size) platform which consumes not as much memory as a Windows OS. This feature is particularly useful when it comes to computing-intensive environment, where a lot of memory and storage spaces are in need. For neuroimaging analysis, it is almost essential that you use a UNIX - based operating system (Mac or Linux), since popular software packages such as FSL, AFNI and FreeSurfer do not run on a Windows operating system.

A number of workstations at the University of Southampton run a *flavour* of Linux operating system known as Red Hat Enterprise Linux (RHEL) 7. Some of these have been configured for neuroimaging analysis. Current machines that can be used for this purpose include:

* uos-15263
* uos-210028
* uos-211997

.. note::

    For more information on the University's RHEL7 machines, see http://linuxdesktops.soton.ac.uk/

Setting Up the Machine
-------------------------

To use the above machines effectively, you need to go through a number of initial set up steps.

0. Grant Access
===============

First of all, your access to the specific University linux workstation needs to be granted. This is typically done by the admin (i.e. you would need to find out who that person is) of that workstation, who will raise an iSolution ticket on behalf of you.

.. note::

    Please provide your UoS username to the admin.

1. Log in
============

These machines can be accessed remotely via remote desktop apps or SSH. 

Remote Desktop Apps
**********************

For MacOS, you can use “Microsoft Remote Desktop”. If you already have it installed for connecting to “Win 10 Student” at the University, then this would come handy. 
For Windows, you can use “Remote Desktop Connection”, which is automatically installed on University machines running Windows.
You should be able to download and install either app on your personal machines.

.. note::

    If you are off site when logging in then you will need to connect to  
    the University's `VPN <https://knowledgenow.soton.ac.uk/Articles/KB0011610>`_ first.

1. On your machine, click on *Start* and search for ``Remote Desktop Connection``
2. Type in the computer name as above and click connect
3. Input your University of Southampton username and password when prompted

Alternatively, if you would like to connect via remote desktop app on Linux, you can use Remmina by following an instruction `here <https://knowledgenow.soton.ac.uk/Articles/KB0020338>`_.

SSH
********************

To connect remotely via SSH, launch a Terminal window, and enter the following command:

.. note::

    If you are off site when logging in then you will need to connect to  
    the University's `VPN <https://knowledgenow.soton.ac.uk/Articles/KB0011610>`_ first.

``ssh username@uos-#.clients.soton.ac.uk`` - Replace ``username`` with your University of Southampton username, and ``#`` with the specific workstation ID.

Please enter your University of Southampton password when prompted, and then hit Return.

To display application GUI's from the remote machine on your computer (e.g. the GUI for FSL or Matlab) you will need to connect with X-forwarding enabled by using
the ``-X`` flag (or on Mac, ``-Y``):

.. code-block:: bash

    ssh -X username@uos-#.clients.soton.ac.uk

Click `here <https://knowledgenow.soton.ac.uk/Articles/KB0011734>`_ for more information on common problems with X and how to solve them.

.. tip::
    
    **What if I am using a Windows machine?**
    
    You can install a terminal emulator and use the commands as above. For example, `MobaXterm <https://mobaxterm.mobatek.net/>`_ has all the features needed to achieve X-forwarding on a Windows machine. Alternatively, you can also use `Git BASH <https://gitforwindows.org/>`_, a BASH emulation used to run Git from the command line, which is already installed on all University Windows machines.

.. tip::

   **I can't connect via SSH and I got a warning message: "REMOTE HOST IDENTIFICATION HAS CHANGED!" What should I do?**
   
   The issue here is most probably due to a new (randomised) host ID has been generated, which is usually a result of system upgrade.
   
   *Why is it causing a warning?*
   
   ssh is warning you that this host ID is different to what it previously saw when you connected to the computer, since it has no way to know whether (as in this case) it is a legitimate change made by the machine owner, or whether someone has maliciously tampered and may be trying to steal information by getting you to connect to a different computer entirely.
   
   *How to solve?*
   
   There are several ways to work around:
       
   1. If this is the only computer that you use ‘ssh’ or related commands (e.g. rsync, scp, sftp) to connect to, then you can safely just delete the file where it keeps its log of host key fingerprints::

        $ rm /h/.ssh/known_hosts
    
    then try the ssh command again, confirm you wish to store the host ID, and proceed as usual.
       
   2. Alternatively, if you wish to preserve the old file, you can rename it to a different filename::
           
        $ mv /h/.ssh/known_hosts rm /h/.ssh/known_hosts_old
           
    then try the ssh command again. In this case, a new known_hosts file will be generated.
       
   3. Alternatively, if you use ssh for other purposes as well (e.g. connect to other computers) and want to keep their host key fingerprints intact, then you will need to delete just the relevant lines from the file. 
   
    You could edit the file with ``vi`` or ``nano`` if you are comfortable with those editors, or, you could use Wordpad or Notepad++ (but not notepad since it is likely not to ‘understand’ the line endings) in Windows, finding the file at ``h:\.ssh\known_hosts``

2. Install Conda
=================
Most of the software you will need has been pre-installed on the machine. However, Conda (a distribution of Python) needs to be installed on a per-user
basis. 

To install conda, first navigate to your home directory:

.. code-block:: bash

    $ cd ~

Then download the installer:

.. code-block:: bash

    $ wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

Then run the installer:

.. code-block:: bash

    $ bash Miniconda3-latest-Linux-x86_64.sh

Follow the prompts on the installer screens. Use ``q`` to skip to the end of the license agreement and accept. When asked,
save conda in a hidden directory in your home directory to prevent other software interfering with it. We suggest:

.. code-block:: bash

    $ ~/.conda/Miniconda3

Once the installer has finished, close and reopen the terminal window. Then type ``conda --version`` to check it has installed successfully.

3. Create a conda environment for your software and analyses
=============================================================

What is a conda environment?
****************************

An environment is a self-contained collection of conda packages. If you change one environment, your other environments and other installed software are not
affected. Some software, particularly DataLad, seems to interfere with other software on the Linux machines. It is therefore safest to use this software
in a self-contained environment.

Conda environments can be easily activated and deactivated as needed.

.. tip::
    
    I have created a ready to use conda environment for neuroimaging. See 
    `below <https://sotnir-handbook.readthedocs.io/en/latest/getting-started/linux-machines.html#install-software>`_

Create your environment
***********************

To create your environment, open a terminal. If conda is installed, you should see that you are currently in the ``base`` environment, 
which is signified like so:

.. code-block:: bash

    (base) [nh6g15@uos-211997 ~] $

Type the following to create a new environment:

.. code-block:: bash

    $ conda create -n myenv

Replace ``myenv`` with whatever you want to call your environment. Press y when prompted to complete the creation.

Activating and deactivating your environment
********************************************

To activate your environment use the following command:

.. code-block:: bash

    $ conda activate myenv

You should now see this environment is active in the terminal, like so:

.. code-block:: bash

    (myenv) [nh6g15@uos-211997 ~] $

You will now be able to use all the software present in this environment.

To deactivate your environment, use the following command:

.. code-block:: bash

    $ conda deactivate

4. Install software
=====================

Much of the software you will need is already present on the machine. However, some software will need to be installed within your newly created 
conda environment. These are:

* DataLad
* Pigz

.. tip::
    
    A ready to use conda environment is available from my `Github page <https://github.com/nhuneke/imagingenv>`_ with instructions on how to install. This environment includes
    DataLad, pigz, and many others such as R studio, dcm2bids, etc.

First activate your conda environment:

.. code-block:: bash

    $ conda activate myenv

Then install each of these software packages with the following:

.. code-block:: bash

    $ conda install -c conda-forge datalad
    $ conda install -c conda-forge pigz

5. Set up FSL 
===============

If this is your first time logging in on the Linux machine then you will need to set up your shell environment to use FSL. 
Each user's shell setup is stored in a file called ``.bash_profile``. Open this file in a text editor:

.. code-block:: bash

    $ gedit ~/.bash_profile

At the end of the file copy and paste the following lines:

.. code-block:: bash

    FSLDIR=/usr/local/fsl    # NOTE: This is default; modify this line to match your local path
    . ${FSLDIR}/etc/fslconf/fsl.sh
    PATH=${FSLDIR}/bin:${PATH}
    export FSLDIR PATH

Then logout and log back in. FSL will now be ready for use.

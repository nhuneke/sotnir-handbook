.. _linux-machines:

=====================
Linux Workstations
=====================
| Contributors: Nathan TM Huneke, Harry Fagan, Nick Hedger, Yukai Zou
| Maintainers: Nathan TM Huneke

--------------

Why Linux?
-------------

For neuroimaging analysis, it is almost essential that you use a UNIX - based operating system (Mac or Linux), 
since popular software packages such as FSL, AFNI and FreeSurfer do not run on a Windows operating system.

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

These machines can be accessed remotely via windows remote desktop or SSH. 

Windows Remote Desktop
**********************

Windows remote desktop is automatically installed on University machines running Windows.
On personal machines you can download and install Windows remote desktop.

.. note::

    If you are off site when logging in then you will need to connect to  
    the University's `VPN <https://knowledgenow.soton.ac.uk/Articles/KB0011610>`_ first.

1. On your machine, click on *Start* and search for ``Remote Desktop Connection``
2. Type in the computer name as above and click connect
3. Input your University of Southampton username and password when prompted

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
    
    You can install a terminal emulator and use the commands as above. `MobaXterm <https://mobaxterm.mobatek.net/>`_ has all the features needed to achieve
    X-forwarding on a Windows machine.

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

    FSLDIR=/usr/local/fsl
    . ${FSLDIR}/etc/fslconf/fsl.sh
    PATH=${FSLDIR}/bin:${PATH}
    export FSLDIR PATH

Then logout and log back in. FSL will now be ready for use.

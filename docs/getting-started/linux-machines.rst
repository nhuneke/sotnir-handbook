.. _linux-machines:

=====================
Linux Workstations
=====================
| Contributors: Nathan TM Huneke, Harry Fagan, Nick Hedger
| Maintainers: Nathan TM Huneke

--------------

Why Linux?
-------------

For neuroimaging analysis, it is almost essential that you use a UNIX - based operating system (Mac or Linux), 
since popular software packages such as FSL, AFNI and FreeSurfer do not run on a Windows operating system.

The University of Southampton provides a number of Linux workstations that run a *flavour* of Linux known as 
Red Hat Enterprise Linux (RHEL) 7. Some of these have been configured for neuroimaging analysis. Current machines
that can be used for this purpose include:

* uos-210028
* uos-211997

.. note::

    For more information on the University's RHEL7 machines, see http://linuxdesktops.soton.ac.uk/

Setting Up the Machine
-------------------------

To use the above machines effectively, you need to go through a number of initial set up steps.

1. Log in
============

These machines can be accessed remotely via windows remote desktop or SSH. Windows remote desktop is automatically installed on University machines running Windows.
On personal machines you can download and install Windows remote desktop.

.. note::

    If you are logging in from a personal machine then you will need to connect to  
    the University's `VPN <https://knowledgenow.soton.ac.uk/Articles/KB0011610>`_.

1. On your machine, click on *Start* and search for ``Remote Desktop Connection``
2. Type in the computer name as above and click connect
3. Input your university of southampton username and password when prompted

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
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An environment is a self-contained collection of conda packages. If you change one environment, your other environments and other installed software are not
affected. Some software, particularly DataLad, seems to interfere with other software on the Linux machines. It is therefore safest to use this software
in a self-contained environment.

Conda environments can be easily activated and deactivated as needed.

Create your environment
~~~~~~~~~~~~~~~~~~~~~~~~~

To create your environment, open a terminal. If conda is installed, you should see that you are currently in the ``base`` environment, 
which is signified like so:

.. code-block:: bash

    (base) [nh6g15@uos-211997 ~] $

Type the following to create a new environment:

.. code-block:: bash

    $ conda create -n myenv

Replace ``myenv`` with whatever you want to call your environment. Press y when prompted to complete the creation.

Activating and deactivating your environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

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
* Dcm2niix
* Dcm2bids

First activate your conda environment:

.. code-block:: bash

    $ conda activate myenv

Then install each of these software packages with the following:

.. code-block:: bash

    $ conda install -c conda-forge datalad
    $ conda install -c conda-forge pigz
    $ conda install -c conda-forge dcm2niix
    $ conda install -c conda-forge dcm2bids

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
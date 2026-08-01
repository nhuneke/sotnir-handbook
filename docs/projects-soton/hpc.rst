.. _hpc:

==========================
High Performance Computing
==========================
| Contributors: Yukai Zou, Nathan Huneke
| Maintainer: Yukai Zou

--------------

.. important::
   
   There is a learning curve ahead. It's important that you first get familiar with operating within a command line interface, and know how to write basic scriptings. More contents and resources of these topics will be added to this handbook.

High Performance Computing (HPC) accelerates large workflows of *highly-interdependent* sub-tasks, which can effectively make the processing and analysis of neuroimage data, especially for large datasets. `The University of Southampton's HPC facility <https://www.southampton.ac.uk/research/facilities/iridis-research-computing-facility>`_ currently comprises multiple systems, including Iridis 6, Iridis X and the newly introduced Iridis 7 platform.

HPC Vocabulary
--------------

What is a Cluster?
~~~~~~~~~~~~~~~~~~

A cluster can be conceptualised as a *system* that consists of three main components:

1. **Hardware**. This includes nodes, interconnection, and storage.
2. **Software**. This includes the operating system, compilers, libraries, applications, and the queue manager that handles the scheduling and execution of tasks.
3. **Infrastructure**. This includes front-end interface, power supply, cooling, data center facility, and technical staff who manage and maintain them.

Clusters are designed to specifically tackle large-scale and computationally intensive problems, such as image processing and simulations. Clusters are widely used in applications such as hydraulic modeling, finance, climate prediction, urban traffic analysis, astronomy, proteomics, and many more.

Node vs. Core
~~~~~~~~~~~~~

A *node* is a *single* computing unit on a cluster. Normally, a node consists of processor(s), memory, storage, and network connectivity that allows the exchange of data and coordination of tasks with other nodes in the cluster.

A *core*, also known as logical processor, is an *individual* compute unit on a physical processor (or CPU, Central Processing Unit).

Below is an example of a node containing two physical processors, each with 10 cores, resulting in a total of 20 logical processors:

.. image:: ../images/node-processors-cores.png
   :width: 400
   :alt: A diagram of a node that consists of two physical processores with ten cores (logical processors) each.

In HPC, the queue manager essentially "sees" logical processors rather than those physical chips (CPUs). Therefore, we will mostly focus on how to make the most of *cores* to help accelerate our workload.

Login Node vs. Compute Node
~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Login node is also known as the front-end node.
- Login node is shared by many users.
- Compute nodes are dedicated resources configured to run computationally intensive workloads.
- Your goal is to get your jobs running at the compute nodes.

Below is a diagram that illustrates differences between login node and compute node:

.. image:: ../images/frontend-vs-compute-nodes.png
   :width: 600
   :alt: Basic components of a cluster, illustrating differences between login and compute nodes.

.. important::

	Overloading login nodes can cause issues for other users. Login nodes are intended for short interactive processing only. For longer, interactive work, please utilise ``sinteractive`` sessions. 

Iridis Open OnDemand
----------------------

For imaging projects, we suggest connecting via Iridis Open OnDemand. This allows you to use interactive apps via a graphical interface, which is almost essential when using FSL or CONN.

Requesting Access
~~~~~~~~~~~~~~~~~~~

You can request access to Iridis Open OnDemand at the `Sharepoint site <https://sotonac.sharepoint.com/teams/HPCCommunityWiki/SitePages/Iridis_Open_OnDemand.aspx>`_

Connecting to Iridis Open OnDemand
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. important::
    
    You must be connected to the University VPN to use Iridis Open OnDemand

Click on ``Connect`` on the `Sharepoint site <https://sotonac.sharepoint.com/teams/HPCCommunityWiki/SitePages/Iridis_Open_OnDemand.aspx>`_.

You will see the following screen:

.. image:: ../images/iridis-connect-screen.png

We suggest opening the ``desktop`` app. Clicking on this will give you several login options:

.. image:: ../images/iridis-connect-options.png

- Node type

    **Login Node**
        Gives up to 2 hours access. *Use this node for Internet access.* When choosing this node the other options below will not apply.

    **Compute Node**
        *No internet access!* Use this node for running compute jobs only.

- Desktop environment: your only option here is xfce
- Partition

    **AMD CPU partition**
        Up to 32 cores for compute jobs

    **L4 GPU partition**
        Required if you plan on using applications with a GUI (e.g. FSL)
        
    **Others**
        Dedicated for ECS

- If choosing the AMD CPU partition, you will be asked how many cores you would like: must be <=32 (3.5GB RAM per core)
- Walltime (hours): must be <= 60 hours
- Name: leave blank

Once you launch your session, a screen summarising it will appear, with a button saying ``Launch Desktop``. Click on this and you will see the xfce environment below:

.. image:: ../images/iridis-xfce.png

When you are done, click on your ``username`` in the top right corner and ``logout``. You can then close the window. 
Request Access
--------------

.. tabs::
    .. group-tab:: For Staff/PGR Students
        Once you have obtained UoS username and password, you will be able to apply for Iridis access after completing an `Iridis Account Application form <https://sotonproduction.service-now.com/serviceportal?id=sc_cat_item&sys_id=bce3a6fa1bf34210e3076351f54bcbe9>`_. The form will ask for a brief justification of usage. If you are uncertain how to fill out the form, please contact your research advisor or line manager.
    .. group-tab:: For Undergraduate/MSc Students
        You can access the Lyceum service and your Project Supervisor/Course Tutor will fill out a `Lyceum Account Application form <https://sotonproduction.service-now.com/serviceportal?id=sc_cat_item&sys_id=2ba3bad5db8f2b00f91c8c994b961961>`_ on your behalf.

Once your access has been granted, you are also subscribed to the HPC mailing list. Make sure to keep an eye on any notice regarding power outage and scheduled maintenance, to ensure your workflow can complete successfully.

Here are a few links to the resources:

- HPC Community Wiki: https://sotonac.sharepoint.com/teams/HPCCommunityWiki
- Submit a job: https://sotonac.sharepoint.com/teams/HPCCommunityWiki/SitePages/Submitting-Jobs-Slurm.aspx
    - Specify job resources: https://sotonac.sharepoint.com/teams/HPCCommunityWiki/SitePages/Submitting-Jobs-Slurm.aspx#specifying-job-resources
- Job extension policy: https://sotonac.sharepoint.com/teams/HPCCommunityWiki/SitePages/Fair-usage-and-Job-extension-policy.aspx

Connect to Iridis
-----------------

To access Iridis, you would need to set up an SSH connection. The methods depend on the operating system you are using.

.. note::

    If you are off site when planning to use Iridis, you will need to connect to  
    the University's `VPN <https://knowledgenow.soton.ac.uk/Articles/KB0011610>`_ first.

.. tabs::
    .. group-tab:: Windows
        You may use clients available for Windows, such as `MobaXterm <https://mobaxterm.mobatek.net/>`_, `PuTTY <https://www.putty.org/>`, or `ThinLinc <https://www.cendio.com/thinlinc>`_. Alternatively, you may run SSH in `Windows Subsystem for Linux <https://learn.microsoft.com/en-us/windows/wsl>`_.
    .. group-tab:: MacOS/Linux
        You can run SSH in `Terminal <https://support.apple.com/en-gb/guide/terminal/welcome>`_ or a Terminal emulator such as `iTerm2 <https://iterm2.com/>`_.

Launching an interactive session
--------------------------------

Interactive jobs allow you to work directly on a compute node for quick testing, such as validating a software or debugging a script.

Initiating an interactive session on a compute node using the ``sinteractive`` command allows for interactive computing and the use of the GUI over X11, e.g. for RStudio, without the risk of overloading the login nodes.

Check out the following page for more details on how to use ``sinteractive``: https://sotonac.sharepoint.com/teams/HPCCommunityWiki/SitePages/Submitting-Jobs-Slurm.aspx#interactive-jobs

Using job arrays
----------------

To run jobs in parallel can greatly accelerate your workflow and save time.

- https://sotonac.sharepoint.com/teams/HPCCommunityWiki/SitePages/Submitting-Jobs-Slurm.aspx#job-arrays
.. _hpc:

==========================
High Performance Computing
==========================
| Contributors: Yukai Zou
| Maintainer: Yukai Zou

--------------

.. note::
	Under construction

High Performance Computing (HPC) accelerates large workflows of *highly-interdependent* sub-tasks, which can effectively make the processing and analysis of neuroimage data (especially large dataset) more efficient. The University of Southampton has one of the largest computational facilities in the UK. `The Iridis Compute Cluster <https://www.southampton.ac.uk/isolutions/staff/iridis.page>`_ is one of the world's top supercomputers, which is now in the 5th generation.

.. important::
   
   There is a learning curve ahead. It's important that you first get familiar with operating within a command line interface, and know how to write basic scriptings. More contents and resources of these topics will be added to this handbook.
   
.. note::

    If you are off site when planning to use Iridis, you will need to connect to  
    the University's `VPN <https://knowledgenow.soton.ac.uk/Articles/KB0011610>`_ first.

Request Access
----------------------

Once you obtain UoS username and password, you will be able to apply for Iridis access after a completing an `online application form <https://sotonproduction.service-now.com/soton/it_rq_iridis_application>`_. The form will ask for a brief justification of usage. 

.. note::
	If you are uncertain how to fill out the form, please contact your research advisor or line manager.
	
Once your access has been granted, you are also subscribed to the HPC mailing list. Make sure to keep an eye on any notice regarding power outage and scheduled maintenance, to ensure your workflow can complete successfully.

Here are a few links to the resources:

- HPC Community Wiki: https://sotonac.sharepoint.com/teams/HPCCommunityWiki
- Submit a job: https://sotonac.sharepoint.com/teams/HPCCommunityWiki/SitePages/Submitting-Jobs-Slurm.aspx
    - Specify job resources: https://sotonac.sharepoint.com/teams/HPCCommunityWiki/SitePages/Submitting-Jobs-Slurm.aspx#specifying-job-resources
- Job extension policy: https://sotonac.sharepoint.com/teams/HPCCommunityWiki/SitePages/Fair-usage-and-Job-extension-policy.aspx

Login nodes
===========


.. important::

	Overloading login nodes can cause issues for other users. Login nodes are intended for short interactive processing only. For longer, interactive work, please utilize ``sinteractive`` sessions. 

Compute nodes
=============

Initiaing an interactive session on a compute node using the ``sinteractive`` command allows for interactive computing and the use of the GUI over X11, e.g. for RStudio, without the risk of overloading the login nodes.

Check out the following page for more details on how to use ``sinteractive``: https://sotonac.sharepoint.com/teams/HPCCommunityWiki/SitePages/Submitting-Jobs-Slurm.aspx#interactive-jobs


Using job arrays
==================

To run jobs in parallel can greatly accelerate your workflow and save time.

- https://sotonac.sharepoint.com/teams/HPCCommunityWiki/SitePages/Submitting-Jobs-Slurm.aspx#job-arrays

Visualisation on Iridis 5
=========================

Although mainly operated in a command line interface, Iridis 5 provides options for visualisation through graphical interface. This section concerns with the option of using `NICE Desktop Cloud Virtualisation <https://nice.soton.ac.uk>`_.

 - Setting up EngineFrame VNC: https://sotonac.sharepoint.com/teams/HPCCommunityWiki/SitePages/Data-Visualisation.aspx#engineframe-vnc

Visualization Expansion Portal (Linux Orange)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In addition to Linux Desktop, Iridis 5 visualisation expansion portal Linux Orange has become available since October 2023. 

+----------------+-------------------------------+
| Nodes          | ``orange02`` and ``orange03`` |
+----------------+-------------------------------+
| Sessions       | 4                             |
+----------------+-------------------------------+
| CPU cores      | 12                            |
+----------------+-------------------------------+
| Memory         | 240 GB                        |
+----------------+-------------------------------+
| GPU available? | No                            |
+----------------+-------------------------------+

(Optional) Mount Research Filestore to Iridis
======================================

The University Research Filestore is a secure research data storage service provided by iSolutions, for the research community to store active research data. Data on the research filestore is backed up and with an extra copy stored in a secure location (for disaster recovery purposes). The newest research filestore supports mounting onto Iridis 5, and this allows a more direct access to the research data via a shared filesystems and network.

.. note::
	Due to the age and the nature of the setup, some research filestore cannot be mounted onto Iridis 5. This is mainly for security reasons. Older research filestore can't set up an NFS export that allows the directory to be mounted in a way that protects the sensitive nature of the data when retrieved via other users on Iridis 5. 
	
	**Solution:** If the data owner requests a new research filestore space, then it can be set up with the old data copied into it. To do this, make a request by filling out a form `here <https://sotonproduction.service-now.com/serviceportal?id=sc_cat_item&sys_id=903e688edbbbf300f91c8c994b961974>`_. iSolution should be able to mount the new filestore to Iridis 5 allow direct access of data.

A100 Scavenger Nodes
--------------------

An A100 scavenger queue has been added to Iridis 5 in December 2023. This queue contains one node and has a twelve hour time limit, and is available to all Iridis 5 users. This may be of interest to users who are interested in testing the A100 GPUs before their full release to the user community.

Specification
=============

+----------------+-----------------------------------------------------------------------+
| GPU hardware   | Dual A100 NVLinked GPUs (160GB VRAM total across two GPUs)            |
+----------------+-----------------------------------------------------------------------+
| CPU hardware   | 48 intel CPUs (24 cores x 2 sockets, Intel(R) Xeon(R) Gold 6336Y CPU  |
|                | @ 2.40GHz)                                                            |
+----------------+-----------------------------------------------------------------------+
| Memory         | 480GB of RAM                                                          |
+----------------+-----------------------------------------------------------------------+

How to access the node
======================

Please use the partition ``a100_scavenger`` to access the node.

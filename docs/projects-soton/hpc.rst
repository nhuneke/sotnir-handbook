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

- Forum: https://hpc.soton.ac.uk/redmine/projects/iridis-5-support/boards
- Wiki: https://hpc.soton.ac.uk/redmine/projects/iridis-5-support/wiki
- Submit a job: https://hpc.soton.ac.uk/redmine/projects/iridis-5-support/wiki/Job_Submission
    - Specify job resources: https://hpc.soton.ac.uk/redmine/projects/iridis-5-support/wiki/Job_Submission#Specifying-Job-Resources

.. note::
	Examples: under construction

Using job arrays
==================

To run jobs in parallel can greatly accelerate your workflow and save time.

- https://hpc.soton.ac.uk/redmine/projects/iridis-5-support/wiki/Job_arrays

Visualisation on Iridis 5
==================

Although mainly operated in a command line interface, Iridis 5 provides options for visualisation through graphical interface. This section concerns with the option of using `NICE Desktop Cloud Virtualisation <https://nice.soton.ac.uk>`_. Information about multi-GPU visualisation can be found `here <https://hpc.soton.ac.uk/redmine/projects/iridis-5-support/wiki/Visualisation>`_.

 - Setting up NICE DCV environment: https://hpc.soton.ac.uk/redmine/projects/iridis-5-support/wiki/Setting_up_NICE_DCV_environment


To obtain access, create a new post under the `Forum: Visualisation Service <https://hpc.soton.ac.uk/redmine/projects/iridis-5-support/boards/25>`_ using the following text:

"Dear HPC Team

Please can you grant me access to NICE Visualisation Service? I am running neuroimaging analyses and would be useful to view intermediate images.

Many thanks

<**Your full name**>"

(Optional Topic) Mount Research Filestore to Iridis
======================================

The University Research Filestore is a secure research data storage service provided by iSolutions, for the research community to store active research data. Data on the research filestore is backed up and with an extra copy stored in a secure location (for disaster recovery purposes). The newest research filestore supports mounting onto Iridis 5, and this allows a more direct access to the research data via a shared filesystems and network.

.. note::
	Due to the age and the nature of the setup, some research filestore cannot be mounted onto Iridis 5. This is mainly for security reasons. Older research filestore can't set up an NFS export that allows the directory to be mounted in a way that protects the sensitive nature of the data when retrieved via other users on Iridis 5. 
	
	**Solution:** If the data owner requests a new research filestore space, then it can be set up with the old data copied into it. To do this, make a request by filling out a form `here <https://sotonproduction.service-now.com/serviceportal?id=sc_cat_item&sys_id=903e688edbbbf300f91c8c994b961974>`_. iSolution should be able to mount the new filestore to Iridis 5 allow direct access of data.
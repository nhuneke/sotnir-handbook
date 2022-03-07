.. _hpc:

=====================
High Performance Computing
=====================
| Contributors: Yukai Zou
| Maintainers: Yukai Zou

--------------

Request Access to Iridis
------------------

Once you obtain UoS credentials (username + password), you will be able to apply for Iridis access after a completing a short form, the link for which is at https://www.southampton.ac.uk/isolutions/staff/iridis.page). 

Here are a few links to Iridis topics:

- https://hpc.soton.ac.uk/redmine/projects/iridis-5-support/boards
- https://hpc.soton.ac.uk/redmine/projects/iridis-5-support/wiki
- https://hpc.soton.ac.uk/redmine/projects/iridis-5-support/wiki/Job_Submission#Specifying-Job-Resources
- https://hpc.soton.ac.uk/redmine/projects/iridis-5-support/wiki/Job_arrays

It is recommended that you subscribe to the mailing list to not miss any notice on maintenance and outage, to ensure your workflow complete successfully.

Submit a job
==================

Run things in parallel: using array for high-throughput computing
==================

(Optional topic) Connect research filestore to Iridis
==================

To do this you would need to first request new generation of the research filestore space from iSolution, which allows connecting to Iridis. The research filestore can be upgraded by [requesting a new space](https://sotonproduction.service-now.com/serviceportal?id=sc_cat_item&sys_id=903e688edbbbf300f91c8c994b961974), to allow direct access of data from Iridis 5. I was told by iSolution that due to the age and the nature of the setup of IanGaleaGroup it couldn’t be mounted. It can be mounted onto Windows machines, but Infrastructure can't set up an NFS export that will allow iSolution to mount the directory in a way that also protects the sensitive nature of the data from access via other users on any Linux system, which includes Iridis 5 unfortunately. However, the newest research filestore supports mounting onto Iridis 5. If the owner of the data requests a new research filestore space, then it can be set up now and the old data copied into it. iSolution should be able to mount this onto Iridis 5 in order to provide a more direct access to the research filestore data. Let me know if this is something you’d like to be considered.


(Optional topic) Visualisation in Iridis
==================

And here’s the link (would need to connect to VPN) regarding [NICE data visualisation](https://nice.soton.ac.uk) on Iridis:
https://hpc.soton.ac.uk/redmine/projects/iridis-5-support/wiki/Visualisation

To request, simply make a new post in the Forum:
https://hpc.soton.ac.uk/redmine/projects/iridis-5-support/boards/25
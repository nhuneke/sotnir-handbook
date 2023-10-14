.. _cloud-computing:

==========================
Cloud Computing
==========================
| Contributors: Yukai Zou
| Maintainer: Yukai Zou

--------------

.. note::
	Under construction

Place holder for intro paragraph. Explain what it is, the benefits, things to consider, and the available options.

UK Biobank Research Analysis Platform (RAP)
-------------------------------------------

.. important::
   You must first have access to a project in UK Biobank. This typically comes with an Application ID, so please reach out to your PI to confirm this.

UK Biobank partners with `DNAnexus <https://www.dnanexus.com/>`_ to provide their cloud computing service, also known as Research Analysis Platform (RAP).

Request Access
**************

1. Register at the UK Biobank Access Management System at https://ams.ukbiobank.ac.uk/ams/, which will take up to 10 working days for approval.

NITRC-CE
--------

Setting up NITRC-CE on AWS Cloud
********************************

1. Visit https://www.nitrc.org/;
2. Click on "CE: Cloud Computing Environment" on top right;
3. Click on "Access NITRC-CE", and select "Find a NITRC-CE AMI" in the drop-down menu;
4. Follow the instructions to set up EC2 instance.
5. (Optional) Under Advanced details, selecting "Request Spot Instances" can take advantage of spare/unused EC2 instances, which significantly reduces cost compared to On-Demand instances.
6. After the instance is launched and status checked, from your EC2 Console Dashboard, copy the Instance ID, visit the Public IPv4 address, and paste the Instance ID into the interface.
7. You will see this screen after login successfully:

.. image:: ../images/nitrc-ce-aws-instance.png
   :width: 600

.. note::
    
    You can also `build your own NITRC-CE instance <https://www.nitrc.org/plugins/mwiki/index.php/nitrc:User_Guide_-_NITRC_Computational_Environment_Getting_Started#Building_Your_Own_NITRC-CE>`_.


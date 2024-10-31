.. _cloud-computing:

==========================
Cloud Computing
==========================
| Contributors: Yukai Zou
| Maintainer: Yukai Zou

--------------

.. note::
	Under construction

Cloud Computing: Basics
-----------------------

According to `Amazon Web Services <https://aws.amazon.com/what-is-cloud-computing/?nc2=h_ql_le_int_cc>`_, cloud computing is the on-demand delivery of IT resources over the Internet with pay-as-you-go pricing. Instead of buying, owning, and maintaining physical data centers and servers, you can access technology services, such as computing power, storage, and databases, on an as-needed basis from a cloud provider.

.. important::
   
   There is a learning curve ahead. Mastering cloud computing requires dedicated effort and practice. To become proficient, you will need to follow a few key steps. First, learn how to request a worker that can do the computational job. Next, set up the software environment and transfer data onto the worker prior to the computation. Finally, specify what computations to run on the worker. If you are stuck, remember to take a break and get back later when your mind is refreshed, or seek assistance from a knowledgable friend!

Working on local machine vs. on cloud
*************************************

+---------------------------------------+---------------------+------------------------+
|                                       | **Working locally** | **Working on cloud**   |
+---------------------------------------+---------------------+------------------------+
| **Who is the owner?**                 | You                 | Cloud service provider |
+---------------------------------------+---------------------+------------------------+
| **Who manages software environment?** | You                 | Cloud service provider |
+---------------------------------------+---------------------+------------------------+
| **Who installs software packages?**   | You                 | You                    |
+---------------------------------------+---------------------+------------------------+
| **Availability of apps and code**     | Yes                 | Transfer needed        |
+---------------------------------------+---------------------+------------------------+
| **Availability of data**              | Yes                 | Tranfer needed         |
+---------------------------------------+---------------------+------------------------+

Instance Types
**************

::

   mem2_ssd1_v2_x16

* ``mem2``: Memory Available per core, ranging from 3.8 GB to 1.9 TB. 
* ``ssd1``: Disk Space Available per core, ranging from 40 GB to 60 TB.
* ``v2``: Versioning. *Always use version 2 of an instance type*.
* ``x16``: Cores/GPUs available, ranging from 2 to 126 cores.

.. note::
    
    **What are the differences between ssd and hdd?**

.. note::
    
    **What are the key things to consider when choosing instance types?**
    
    - Whether your software requires more memory (``mem2`` vs. ``mem3``)
    - Whether your software requires large storage space (``ssd1`` vs. ``ssd2``)
    - Whether your software utilises multiple cores (``x16`` vs. ``x32``)
    - Whether your software is GPU optimised (``gpu_x32``)

UK Biobank Research Analysis Platform (RAP)
-------------------------------------------

.. important::
   You must first have access to a project in UK Biobank. This typically comes with an Application ID, so please reach out to your PI to confirm this.

UK Biobank partners with `DNAnexus <https://www.dnanexus.com/>`_ to provide their cloud computing service, also known as Research Analysis Platform (RAP).

Request Access
**************

1. Register at the UK Biobank Access Management System at https://ams.ukbiobank.ac.uk/ams/, which will take up to 10 working days for approval.

Image Processing on RAP
***********************

DXJupyterLab App is a DNAnexus extension that allows JupyterLab server to directly view and interact with DNANexus projects, and allows analyses to be carried out in a Jupyter notebook running on the DNAnexus platform. You can simply connect to the Jupyter environment using a local web browser.

JupyterLab app with IMAGE_PROCESSING feature provides access to the following Python libraries:

* ``Nipype (1.8.4)``: click `here <https://miykael.github.io/nipype_tutorial/>`__ for a very good Nipype tutorial.
* ``FreeSurfer (7.3.2)``
* ``FSL (3.2.3)``

A full list of individual apps and tools is available at the `Tools Library documentation <https://dnanexus.gitbook.io/uk-biobank-rap/working-on-the-research-analysis-platform/tools-library>`_.


To launch DXJupyterLab on RAP's user interface:

1. Click on Projects on the navigation bar, and select a project in which you wish to run this app. 
2. Click the Start Analysis button.
3. From the list of tools, select "JupyterLab with Python, R, Stata, ML, Image Processing)".

To launch DXJupyterLab from the command line, run:

::

   dx run dxjupyterlab
   dx run dxjupyterlab -h # List instructions for specifying inputs

:: important::
   You will first need to set up the ``dx`` command-line client. Click `here <https://documentation.dnanexus.com/getting-started/cli-quickstart>`__ for a quickstart.

Costs and Billing
*****************

You can use the AWS estimator `here <https://calculator.aws>`__ to obtain an estimated cost. Detailed information about rates of different instance types is available `here <https://20779781.fs1.hubspotusercontent-na1.net/hubfs/20779781/Product%20Team%20Folder/Rate%20Cards/BiobankResearchAnalysisPlatform_Rate%20Card_Current.pdf>`__. 

NeuroImaging Tools & Resourcees Collaboratory (NITRC)
-----------------------------------------------------

NeuroImaging Tools & Resourcees Collaboratory (NITRC, https://nitrc.org) is a free web-based resource that offers comprehensive information on neuroinformatics software and data. To date, more than 1,000 neuroimaging tools and resources have been registered, and NITRC has become the *de facto* standard mechanism for sharing neuroimaging tools and resources. NITRC contains three main components: Resource Registry (NITRC-RR), Imaging Repository (NITRC-IR), and Computational Environment (NITRC-CE).

NITRC-CE: the Computational Environment
***************************************

NITRC-CE provides a cloud-based, pay-as-you-go virtual computing platform. It is pre-configured with popular neuroimaging tools, including FSL, FreeSurfer, ANTs, C-PAC, MRIcron, etc. A full list of the installed packages is available `here <https://www.nitrc.org/plugins/mwiki/index.php/nitrc:User_Guide_-_NITRC_Computational_Environment_Installed_Packages>`__. Additionally, you can also add your own commercial or open source tools.

Installed Packages
******************

Below are the packages already installed for NITRC-CE (v0.57-14):

.. list-table:: 
    :widths: 10 10 50
    :header-rows: 1
    :stub-columns: 1

    * - Package
      - Version
      - Description
    * - 3D Slicer
      - 4.11.20210226
      - 3D Slicer Decription
    * - AFNI
      - AFNI_24.0.15
      - A collection of tools for processing and analyzing functional MRI data.
    * - ANTS
      - 2.4.2
      - Image registration and segmentation tool for medical imaging.
    * - BrainSuite
      - 16a1
      - A software for analysing structural MRI images of the brain.
    * - CONN
      - 22a
      - A MATLAB-based software for fMRI analysis.
    * - C-PAC
      - 1.8.6
      - A pipeline for reproducible fMRI data processing and analysis.
    * - DataLad
      - 0.19.5-1~nd22.04+1
      - A data management tool that streamlines seamless data access versioning, and sharing for scientific research.
    * - Docker
      - 24.0.2
      - A platform for developing, deploying, and executing applications in a containerised and reproducible environment.
    * - DTIPrep
      - 1.2.4
      - A tool for quality control and preprocessing of diffusion tensor imaging (DTI) data.
    * - EEGLAB
      - v2023.1
      - An interactive MATLAB-based toolbox for processing and analysing EEG data.
    * - FreeSurfer
      - 7.2.0
      - A popular software for neuroimaging analysis.
    * - FSL
      - 6.0.7.9
      - A popular and comprehensive library of tools for analysing MRI neuroimaging data.
    * - HeuDiConv
      - 0.13.1-1~nd22.04+1
      - A DICOM converter for organizing and converting neuroimaging data into NIfTI format that are BIDS-compliant.
    * - HTCondor
      - 10.0.9-1.1
      - A high-throughput computing software for distributed task scheduling and resource management.
    * - MaCH
      - 1.0.18.c
      - A Markov Chain based tool for haplotype estimation and genotype imputation in genetics research.
    * - MRIcron
      - 1.2.20211006+dfsg-1
      - A tool for viewing neuroimaging data and converting image data formats.
    * - MRtrix
      - 3.0.3-1
      - A popular tool for processing, analyzing, and visualizing diffusion MRI data.
    * - NeuroDocker
      - 0.9.4
      - A command-line program that creates custom Dockerfiles and Singularity images for neuroimaging software.
    * - NEURON
      - 7.6.3-1build6
      - A simulation environment for modeling neurons and networks of neurons.
    * - PLINK!
      - v1.07
      - A collection of tools for genome-wide association studies and population genetics analysis.
    * - Pydicom
      - 2.2.2-1
      - A Python package for working with DICOM medical image files.
    * - dipy
      - 1.4.1-1build1
      - A popular python library for analysing diffusion MRI data.
    * - NiBabel
      - 3.2.2-1
      - A python library for accessing and transforming neuroimaging data formats.
    * - NIPY
      - 0.5.0
      - A python project that provides tools for processing and analysis of neuroimaging data.
    * - NiPype
      - 1.7.0-1
      - A python library for creating reproducible and flexible neuroimaging workflows.
    * - Singularity
      - 3.7.3
      - A container platform designed for high-performance computing and reproducible research.
    * - SOLAR-Eclipse
      - 8.4.2
      - A statistical software for genetic and linkage analysis.
    * - SPM
      - 12
      - A popular MATLAB-based software package for brain imaging analysis, especially for PET and fMRI data.
    * - TrackVis
      - 0.6.1
      - A tool for visualising and analysing fiber tracks of diffusion MRI data.

Setting up NITRC-CE on Amazon Web Services (AWS)
************************************************

.. note::
    
    You can `build your own NITRC-CE instance <https://www.nitrc.org/plugins/mwiki/index.php/nitrc:User_Guide_-_NITRC_Computational_Environment_Getting_Started#Building_Your_Own_NITRC-CE>`_.

Using NITRC-CE on AWS is a straightforward process and can save substantial time setting up a computational environment for neuroimaging data analysis.

1. Visit https://www.nitrc.org/;
2. Click on "CE: Cloud Computing Environment" on top right;
3. Click on "Access NITRC-CE", and select "Find a NITRC-CE AMI" in the drop-down menu;
4. Follow the instructions to set up EC2 instance.
5. (Optional) Under Advanced details, selecting "Request Spot Instances" can take advantage of spare/unused EC2 instances, which significantly reduces cost compared to On-Demand instances.
6. After the instance is launched and status checked, from your EC2 Console Dashboard, copy the Instance ID, visit the Public IPv4 address, and paste the Instance ID into the interface.

You will see this screen after login successfully:

.. image:: ../images/nitrc-ce-aws-instance.png
   :width: 600

AWS EC2 Pricing
***************

Pricing information for using AWS EC2 instances is available `here <https://aws.amazon.com/ec2/pricing>`_.
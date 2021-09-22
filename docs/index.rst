.. SOTNIR handbook documentation master file, created by
   sphinx-quickstart on Mon Jul 26 16:21:07 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to the SOTNIR handbook!
===========================================

This handbook is a resource for those carrying out neuroimaging projects.

This resource contains quickstart guides, example scripts, and standardised workflows, developed in Southampton.

Contributors are credited on each page.

.. important::
   
   If you would like to contribute to this handbook, please contact Nathan (N.Huneke@soton.ac.uk), Ara (A.Varatharaj@soton.ac.uk), or Kai (Y.Zou@soton.ac.uk)

.. toctree::
   :maxdepth: 1
   :caption: Getting started
   
   getting-started/linux-machines.rst
   getting-started/unix-basics.rst
   getting-started/BIDS.rst
   getting-started/datalad.rst
 
.. toctree::
   :maxdepth: 1
   :caption: Getting Access to Clinical Data at UHS

   XNAT/intro.rst
 
.. toctree::
   :maxdepth: 1
   :caption: Undertaking a Neuroimaging Project in Southampton

   projects-soton/intro.rst
   projects-soton/mri-scanner.rst

.. toctree::
   :maxdepth: 1
   :caption: File conversion

   conversion/convert2nifti.rst
   conversion/pydeface.rst

.. toctree::
   :maxdepth: 1
   :caption: fMRI Preprocessing with fMRIPrep

   fmriprep/intro.rst
   fmriprep/convert2nifti.rst
   fmriprep/install-fmriprep.rst
   fmriprep/running-fmriprep.rst

.. toctree::
   :maxdepth: 1
   :caption: fMRI Analysis

   fmri-analysis/intro.rst

.. toctree::
   :maxdepth: 1
   :caption: Functional connectivity analyses

   connectivity/intro.rst

.. toctree::
   :maxdepth: 1
   :caption: Diffusion Tensor Imaging

   dti/intro.rst

.. note::
	Under construction. When new sections are completed they will be listed here.
	
	26/07/2021 - version 0.1.0

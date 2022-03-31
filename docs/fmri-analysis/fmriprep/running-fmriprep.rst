.. _running-fmriprep.rst:

==============================================
Running fMRIPrep
==============================================
| Contributors: Nathan TM Huneke
| Maintainers: Nathan TM Huneke

----------------------------------------------

fMRIPrep is best run as a docker image and using the fmriprep-docker wrapper.

If you are using my :ref:`neuroimaging conda environment <getting-started/linux-machines:3. create a conda environment for your software and analyses>` 
then the fmriprep-docker wrapper will already be installed. 

.. warning:: 
    
    You should pre-process all participants in a study using the **same** version 
    of fMRIPrep!

The ``fmriprep-docker`` command has many available arguments, but for our purposes
most are not relevant. I suggest you use the following:

.. code-block:: bash

    fmriprep-docker \
        path/to/bids/directory \
        path/to/output/directory \
        participant  \
        --participant-label 01 \
        --user $( id -u ) \
        --skip-bids-validation \
        --fs-license-file /local/software/freesurfer/license.txt

.. todo:: 

    Finish page

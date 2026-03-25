.. _running-fmriprep.rst:

==============================================
Running fMRIPrep
==============================================
| Contributors: Nathan TM Huneke
| Maintainers: Nathan TM Huneke

----------------------------------------------

.. danger:: 
    
    You should pre-process all participants in a study using the **same** version 
    of fMRIPrep!

fMRIPrep is best run as a docker image and using the fmriprep-docker wrapper.

If you are using my :ref:`neuroimaging conda environment <getting-started/linux-machines:3. create a conda environment for your software and analyses>` 
then the fmriprep-docker wrapper will already be installed. 

.. note::

    If you are using a university machine then you will need to be given permission to
    use Docker. Please speak to the admin for the machine.


The fMRIPrep-Docker command
-----------------------------

.. warning:: 

    Preprocessing each participant with fMRIPrep takes approximately 6-12 hours. 
    Plan your time accordingly.

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

There are a few arguments to explain here:

- replace ``path/to/bids/directory`` with the actual path to your BIDS directory
- replace ``path/to/output/directory`` with the path you would like for your outputs
- ``participant`` means do pre-processing at the participant as opposed to group level
- ``--participant-label`` is the subject ID (i.e. the label after ``sub-``)
- ``--user`` defines which user should own the outputs. ``$( id -u )`` represents your username, so that you will own all the outputs. By default fmriprep-docker will run as root which is unhelpful on a shared machine
- ``--skip-bids-validation`` prevents an error when using datalad datasets
- ``--fs-license-file`` specifies the location of the freesurfer license file, which is needed for surface reconstruction. The location above is correct for the university linux machines and does not need to be changed

Using fMRIPrep on Iridis Open OnDemand
---------------------------------------

On the HPC cluster, rather than using ``Docker`` you will need to run fMRIPrep in ``Apptainer``. You can see more about using Apptainer on Iridis `here <https://sotonac.sharepoint.com/teams/HPCCommunityWiki/SitePages/Apptainer.aspx?web=1>`_.

Install the image
~~~~~~~~~~~~~~~~~~

.. important::

    You will need to be using the login node for internet access to install the image

Open a terminal and load the module:

.. code-block:: bash

    module load apptainer

Next you will need to download the image:

.. code-block:: bash

    apptainer pull ~/my_images/fmriprep-latest.sif \ 
        docker://nipreps/fmriprep:latest

If you need to download a specific version of fmriprep, then replace ``latest`` with the version number you require in the command above.

Run fMRIPrep with Apptainer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. important::

    Logout and log back in to Iridis on a compute node. Remember to re-load the Apptainer module when logging back in.

Unfortunately there is no python wrapper for fMRIPrep to use with Apptainer, so the command is slightly more complex.

.. code-block:: bash

    apptainer run --unsquash \
        --bind path/to/bids/directory:/data \
        --bind path/to/scratch:/scratch \
        ~/my_images/fmriprep-latest.sif \
        /data/sub-01 \
        /data/sub-01/derivatives/fmriprep \
        participant \
        --participant-label 01 \
        --skip-bids-validation \
        --fs-license-file /home/nh6g15/freesurfer/license.txt \
        --work-dir /scratch/nh6g15/fmriprep_work

The first part of the command, until the ``path/to/image.sif`` are apptainer related arguments: 

- ``unsquash`` avoids using squashfs. We found this tends to work better on Iridis.
- ``bind`` tells apptainer to bind directories to certain paths within the image. You will need to ``bind`` your ``BIDS`` directory and ``scratch`` (if both are in ``scratch`` then only bind once)

Following this, hopefully the command appears familiar. This is essentially the command we passed to ``fmriprep-docker``.

.. important::

    We suggest using all 32 cores available to you in the AMD compute nodes. Processing each participant will take 2-3 hours.

Inspecting the Outputs
-------------------------

The outputs of fMRIPrep will be saved in your ``output directory`` in two directories:
``fmriprep`` and ``freesurfer``.

Outputs are structured as follows within the ``fmriprep`` directory::

    fmriprep/
        dataset_description.json
        desc-aparcaseg_dseg.tsv
        desc-aseg_dseg.tsv
        logs/
        sub-01.html
        sub-01/
            anat/
            figures/
            log/
            ses-01/
                anat/
                func/
                    sub-01_ses-01_task-faces_desc-confounds_timeseries.json
                    sub-01_ses-01_task-faces_desc-confounds_timeseries.tsv
                    sub-01_ses-01_task-faces_from-scanner_to-T1w_mode-image_xfm.txt
                    sub-01_ses-01_task-faces_from-T1w_to-scanner_mode-image_xfm.txt
                    sub-01_ses-01_task-faces_space-MNI152NLin2009cAsym_boldref.nii.gz
                    sub-01_ses-01_task-faces_space-MNI152NLin2009cAsym_desc-aparcaseg_dseg.nii.gz
                    sub-01_ses-01_task-faces_space-MNI152NLin2009cAsym_desc-aseg_dseg.nii.gz
                    sub-01_ses-01_task-faces_space-MNI152NLin2009cAsym_desc-brain_mask.nii.gz
                    sub-01_ses-01_task-faces_space-MNI152NLin2009cAsym_desc-brain_mask.json
                    sub-01_ses-01_task-faces_space-MNI152NLin2009cAsym_desc-preproc_bold.nii.gz
                    sub-01_ses-01_task-faces_space-MNI152NLin2009cAsym_desc-preproc_bold.json
            ses-02/
        sub-02.html
        sub-02/
        sub-03.html
        sub-03/
        ...
        etc.

Your preprocessed BOLD data is ``sub-01_ses-01_task-faces_space-MNI152NLin2009cAsym_desc-preproc_bold.nii.gz``. 
Brain extraction is not performed on these data, but a brain mask (``sub-01_ses-01_task-faces_space-MNI152NLin2009cAsym_desc-brain_mask.nii.gz``) is created and can be used later.

fMRIPrep produces a very useful html report for each participant in the top level directory called ``sub-id.html``.
You should inspect this report to see whether there have been any errors and whether the preprocessing has
been performed well. A guide for exploring these reports and interpreting the images is available `here <https://github.com/nimh-comppsych/fmriprep_qa_guide>`_.


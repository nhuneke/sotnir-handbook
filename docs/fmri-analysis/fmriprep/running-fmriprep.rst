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

- ``participant`` means do pre-processing at the participant as opposed to group level
- ``--participant-label`` is the subject ID (i.e. the label after ``sub-``)
- ``--user`` defines which user should own the outputs. ``$( id -u )`` represents your username, so that you will own all the outputs. By default fmriprep-docker will run as root which is unhelpful on a shared machine
- ``--skip-bids-validation`` prevents an error when using datalad datasets
- ``--fs-license-file`` specifies the location of the freesurfer license file, which is needed for surface reconstruction

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


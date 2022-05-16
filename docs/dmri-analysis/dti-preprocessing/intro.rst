.. _fmriprep.rst:

==============================================
DTI Preprocessing with FSL
==============================================
| Contributors: Yukai Zou, Ikbeom Jang
| Maintainers: Yukai Zou

------------------------------------------

.. note::

    Under construction

Download and Organize Data
--------------------------

Scripts to download and organize PNG's MRI data (e.g. DTI) can be accessed at https://github.com/jibikbam/Download-and-organize-MRI-data-in-bash.

Preprocess Data
---------------

Scripts to preprocess DTI can be accessed at https://github.com/jibikbam/DTI-process-analysis. You may use them if you'd like to try the easiest path.

- Make sure you have ``acqparams.txt``, ``index.txt``, and ``DICOM`` files. The number of values in ``index.txt`` should match the number of diffusion encoding directions of the data you use.
- Run the processing script with the command ``bash process_DTI.sh``.
- The eddy current correction requires the longest time, therefore, it is recommended to process in parallel by using ``eddy_openmp`` (multi CPU core) or ``eddy_cuda9.1`` (GPU). Download one depending on the hardware resource available.
- DTI outputs should be ready including FA, MD, L1, L2, L3 images.
- To visualize output images, use FSL's ``fsleyes``. You may also use FreeSurfer's freeview or AFNI viewer, etc. You may also visualize them in MATLAB or Python using some libraries (see DTI Analysis).

.. note::

    Some parameters may need to change depending on the data you use. But for now, don't worry about it too much and focus on making it run.

.. note::

    The processing can be improved in several ways. For example, use T1 or T2 for brain extraction rather than using b=0 volume of DTI (i.e. vol0000.nii.gz). Use the ``topup`` option in eddy for correcting susceptibility induced distortions if your DTI sequence collected two b=0 volumes with different phase encoding directions. 

Tract-Based Spatial Statistics (TBSS)
-------------------------------------

.. important::

    You can stop here if the purpose is to get FA and MD images of each individual. Below are further steps in case you need them.

TBSS extracts white matter tracts. It should be straightforward to follow the TBSS steps described in FSL's documentation page `here <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/TBSS/UserGuide>`_.
- If you just need skeletonized FA co-registered between all subjects, follow steps until "voxelwise statistics on the skeletonised FA data" section.
- If you need other metrics such as MD, AD, or RD, follow until "Using non-FA Images in TBSS".
- Feel free to do further steps as needed.


.. _fmriprep.rst:

==============================================
DTI Preprocessing with FSL
==============================================
| Contributors: Yukai Zou, Ikbeom Jang
| Maintainers: Yukai Zou

.. contents:: **Contents**
    :local:

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

Eddy Current Correction
************************

Before running eddy current correction, make sure you have ``acqparams.txt`` and ``index.txt`` files. 

Preparing ``acqparams.txt``
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Each row of the file contains four elements. The first three elements are the phase encoding direction.

The fourth element in each row is the time (in seconds) between reading the center of the first echo and reading the center of the last echo. It can be computed in several ways:

.. tabs::

    .. tab:: Method 1

        It is the "dwell time" (in seconds) multiplied by "number of PE steps - 1":

        .. code-block:: b

            "DwellTime": 2.6e-06,
            "NumberOfPhaseEncodingSteps": 95,

    .. tab:: Method 2

        It is also the reciprocal of the PE bandwidth/pixel:

        .. code-block:: b

            "BandwidthPerPixelPhaseEncode": 20.833,

    .. tab:: Method 3

        For a Siemens scanner you will get a "protocol PDF" that contains all the relevant information. Look for the tags "Phase enc. dir.", "Echo spacing" and "EPI factor". Here is an example:

        .. code-block:: b

            "PhaseEncodingDirection": "j-",
            "EchoSpacing": 0.000750012,
            "EffectiveEchoSpacing": 0.000375006,
            "ParallelReductionFactorInPlane": 2,

Preparing ``index.txt``
~~~~~~~~~~~~~~~~~~~~~~~

This file can be created by passing a text file with the number of ones that match the number of phase encoding directions of the data you use. 

For example, if the data you use contains 64 volumes acquired with A to P phase encoding direction, the ``index.txt`` file should contain 64 ones. Such a file can be created by running the following commands:

.. code-block:: b
    indx=""
    for ((i=1; i<=64; i+=1)); do indx="$indx 1"; done
    echo $indx > index.txt

Tract-Based Spatial Statistics (TBSS)
-------------------------------------

.. important::

    You can stop here if the purpose is to get FA and MD images of each individual. Below are further steps in case you need them.

TBSS extracts white matter tracts. It should be straightforward to follow the TBSS steps described in FSL's documentation page `here <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/TBSS/UserGuide>`_.

- If you just need skeletonized FA co-registered between all subjects, follow steps until "voxelwise statistics on the skeletonised FA data" section.
- If you need other metrics such as MD, AD, or RD, follow until "Using non-FA Images in TBSS".
- Feel free to do further steps as needed.


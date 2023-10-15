.. _convert2nifti.rst:

====================================
Convert from DICOM to NIfTI
====================================
| Contributors: Nathan TM Huneke, Harry Fagan, Yukai Zou
| Maintainers: Nathan TM Huneke

------------------------------------------

A common preprocessing step in neuroimaging data analysis is converting DICOM (Digital Imaging and Communications in Medicine) format output by the scanner to NIfTI (Neuroimaging Informatics Technology Initiative) format. This comes with several benefits, including a more standardised format for neuroimaging data, more consistent data format across multiple imaging modalities and scanners, enhanced compatibility with a wide range of neuroimaging software, and a more streamlined workflow for data analysis and sharing.

Dcm2niix
--------

::

    dcm2niix -b o -r y -w 1 -o /path/to/destination -f sub-$sID/%t_s%2s_%d/%d_%5r.dcm /path/to/inputdata

- ``-b`` refers to BIDS sidecar, which is set to ``o`` to indicate there is no NIfTI.
- ``-r`` is set to ``y``, to rename instead of convert DICOMs.
- ``-w`` is set to ``1`` to overwrite wherever name conflicts occur.
- ``-f`` specifies how the output filename will look like.

Dcm2bids
--------

It would be a good practice to organise the NIfTI data in compliance with the BIDS (Brain Imaging Data Structure) standard. To do this, we suggest using an app called `dcm2bids <https://unfmontreal.github.io/Dcm2Bids/>`_.

If you are using my :ref:`neuroimaging conda environment <getting-started/linux-machines:3. create a conda environment for your software and analyses>` 
then dcm2bids and its dependencies will already be installed. 

The Dcm2bids Helper
*******************

The scanner will output a number of original and derived series, most of which
are not required for further analysis and do not need to be stored in the BIDS tree.
Those that are required need to be placed in the correct part of the directory tree, along with 
their JSON sidecar files. How is this achieved? The Dcm2bids helper will
run a dummy conversion, allowing you to see all the series in NIfTI format their JSON
sidecar files. You can then decide which ones to keep and build a configuration file
that will automatically place the correct images in their corresponding places in
the directory tree.

Here is an example of some source data from the scanner for a single subject: ::

    study/
        sourcedata/
            sub-01/
                2/
                    IM-0001-0001.dcm
                    IM-0001-0002.dcm
                    IM-0001-0003.dcm
                    ...
                3/
                4/
                5/
                6/
                7/
                8/
                9/
                10/
                11/
                12/
                13/
                14/
                15/
                16/
                17/
                18/
                19/
                20/

Each directory within ``sub-01/`` is a series containing a number of DICOM images.
At the moment they don't mean much to us. Now if we run the Dcm2bids helper with

.. code-block:: bash

    dcm2bids_helper -d sub-01 -o ../bids/

This creates a directory within the specified output directory ``bids/`` called
``tmp_dcm2bids/helper/``. Let's have a look inside this directory: ::

    study/
        sourcedata/ 
            sub-01/
        bids/
            tmp_dcm2bids/
                helper/
                    002_study_t1_mprage_sag_p2_iso_1.0_20180512142245.json
                    002_study_t1_mprage_sag_p2_iso_1.0_20180512142245.nii.gz
                    003_study_ep2d_diff_b1300_iso2p4_phase_AP_36dir_20180512142245.bval
                    003_study_ep2d_diff_b1300_iso2p4_phase_AP_36dir_20180512142245.bvec
                    003_study_ep2d_diff_b1300_iso2p4_phase_AP_36dir_20180512142245.json
                    003_study_ep2d_diff_b1300_iso2p4_phase_AP_36dir_20180512142245.nii.gz
                    004_study_ep2d_diff_b1300_iso2p4_phase_AP_36dir_20180512142245.json
                    004_study_ep2d_diff_b1300_iso2p4_phase_AP_36dir_20180512142245.nii.gz
                    005_study_ep2d_diff_b1300_iso2p4_phase_AP_36dir_20180512142245.bval
                    005_study_ep2d_diff_b1300_iso2p4_phase_AP_36dir_20180512142245.bvec
                    005_study_ep2d_diff_b1300_iso2p4_phase_AP_36dir_20180512142245.json
                    005_study_ep2d_diff_b1300_iso2p4_phase_AP_36dir_20180512142245.nii.gz
                    006_study_ep2d_diff_b1300_iso2p4_phase_AP_36dir_20180512142245.json
                    006_study_ep2d_diff_b1300_iso2p4_phase_AP_36dir_20180512142245.nii.gz
                    007_study_ep2d_diff_b1300_iso2p4_phase_AP_36dir_20180512142245.json
                    007_study_ep2d_diff_b1300_iso2p4_phase_AP_36dir_20180512142245.nii.gz
                    009_study_gre_field_mapping_2.5mm_20180512142245_e1.json
                    009_study_gre_field_mapping_2.5mm_20180512142245_e1.nii.gz
                    009_study_gre_field_mapping_2.5mm_20180512142245_e2.json
                    009_study_gre_field_mapping_2.5mm_20180512142245_e2.nii.gz
                    010_study_gre_field_mapping_2.5mm_20180512142245_e2_ph.json
                    010_study_gre_field_mapping_2.5mm_20180512142245_e2_ph.nii.gz
                    011_study_ep2d_bold_moco_p4_2.5mm_TR2500_378_REST_20180512142245.json
                    011_study_ep2d_bold_moco_p4_2.5mm_TR2500_378_REST_20180512142245.nii.gz
                    012_study_ep2d_bold_moco_p4_2.5mm_TR2500_378_REST_MoCo_20180512142245.json
                    012_study_ep2d_bold_moco_p4_2.5mm_TR2500_378_REST_MoCo_20180512142245.nii.gz
                    013_study_ep2d_bold_moco_p4_2.5mm_TR2500_378_REST_20180512142245.json
                    013_study_ep2d_bold_moco_p4_2.5mm_TR2500_378_REST_20180512142245.nii.gz
                    014_study_ep2d_bold_moco_p4_2.5mm_TR2500_378_REST_MoCo_20180512142245.json
                    014_study_ep2d_bold_moco_p4_2.5mm_TR2500_378_REST_MoCo_20180512142245.nii.gz
                    015_study_ep2d_bold_moco_p4_2.5mm_TR2500_378_REST_MoCo_20180512142245.json
                    015_study_ep2d_bold_moco_p4_2.5mm_TR2500_378_REST_MoCo_20180512142245.nii.gz
                    016_study_ep2d_bold_moco_p4_2.5mm_TR2500_178_FACES_20180512142245.json
                    016_study_ep2d_bold_moco_p4_2.5mm_TR2500_178_FACES_20180512142245.nii.gz
                    017_study_ep2d_bold_moco_p4_2.5mm_TR2500_178_FACES_MoCo_20180512142245.json
                    017_study_ep2d_bold_moco_p4_2.5mm_TR2500_178_FACES_MoCo_20180512142245.nii.gz
                    018_study_ep2d_bold_moco_p4_2.5mm_TR2500_178_FACES_20180512142245.json
                    018_study_ep2d_bold_moco_p4_2.5mm_TR2500_178_FACES_20180512142245.nii.gz
                    019_study_ep2d_bold_moco_p4_2.5mm_TR2500_178_FACES_MoCo_20180512142245.json
                    019_study_ep2d_bold_moco_p4_2.5mm_TR2500_178_FACES_MoCo_20180512142245.nii.gz
                    020_study_ep2d_bold_moco_p4_2.5mm_TR2500_178_FACES_20180512142245.json
                    020_study_ep2d_bold_moco_p4_2.5mm_TR2500_178_FACES_20180512142245.nii.gz

This makes a bit more sense. We can see this study is made up of a T1-weighted anatomical scan, DTI, field mapping, fMRI at rest and during
a faces task. Not all of these series are original scans, some are derived by the scanner. It is the original scans we need
for further analysis. Opening up the JSON sidecar files can give more information. 

Configuring Dcm2bids
********************

To tell Dcm2bids which images are anatomical, DTI, etc. we need to create a configuration JSON file. 
This file should be kept in your dataset in a directory called ``code/``. Here is an example configuration file
based on this study:

.. code-block:: json

    {
        "descriptions": [
            {
            "dataType": "anat",
            "modalityLabel": "T1w",
            "criteria": {
                "SeriesDescription": "t1_mprage_sag_p2_iso_1.0"
                }
            },
            {
            "dataType": "dwi",
            "modalityLabel": "dwi"
            "criteria": {
                "SidecarFilename": "003_*"
                }
            },
            {
            "dataType": "fmap",
            "modalityLabel": "magnitude1",
            "IntendedFor": [
                5,
                6
            ],
            "criteria": {
                "SeriesDescription": "gre_field_mapping_2.5x2.5x3",
                "EchoNumber": 1
                }
            },
            {
            "dataType": "fmap",
            "modalityLabel": "magnitude2",
            "IntendedFor": [
                5,
                6
            ],
            "criteria": {
                "SidecarFilename": "*_e2.json"
                }
            },
            {
            "dataType": "fmap",
            "modalityLabel": "phasediff",
            "IntendedFor": [
                5,
                6
            ],
            "criteria": {
                "SidecarFilename": "*_e2_ph.json"
                }
            },
            {
            "dataType": "func",
            "modalityLabel": "bold",
            "customLabels": "task-rest",
            "criteria": {
                "SeriesDescription": "ep2d_bold_moco_p4_2.5mm_TR2500_378_REST",
                "ImageType": [
                    "ORIGINAL",
                    "PRIMARY",
                    "FMRI",
                    "NONE",
                    "ND",
                    "MOSAIC"
                    ]
                },
            "sidecarChanges": {
                "TaskName": "rest"
                }
            },
            {
            "dataType": "func",
            "modalityLabel": "bold",
            "customLabels": "task-faces",
            "criteria": {
                "SeriesDescription": "ep2d_bold_moco_p4_2.5mm_TR2500_178_FACES",
                "ImageType": [
                    "ORIGINAL",
                    "PRIMARY",
                    "FMRI",
                    "NONE",
                    "ND",
                    "MOSAIC"
                    ]
                },
            "sidecarChanges": {
                "TaskName": "faces"
                }
            }
        ]
    }

The idea behind this configuration file is that Dcm2bids will search through all of the JSON sidecar files
during the conversion and look for matches with the ``criteria`` specified in the configuration file. 
Wherever a match is found, that NIfTI file and its JSON sidecar will be moved to the correct place in the BIDS
tree. It is important therefore that the ``criteria`` you specify apply *to one scan only*. Otherwise Dcm2bids 
will show an error.

The ``customLabels`` fields are used to name the files after conversion. Use ``customLabels`` to add information, e.g. task name, 
after the modality label. Dcm2bids will use information in ``sidecarChanges`` to write
lines into the converted NIfTI file's corresponding JSON sidecar. This is important for adding task names for BOLD 
runs, a BIDS requirement. You can also add other extra information if needed.

The least intuitive field is the ``IntendedFor`` field. In the example above, this field is a list describing which scans
the field map applies to. In this case it is each of the BOLD runs, which are the 6th and 7th scans described in the file.
The configuration file counts up from 0, so in our file above, the number for each scan is as follows: ::

    T1w (0)
    DTI (1)
    Fieldmap 1st echo (2)
    Fieldmap 2nd echo (3)
    Fieldmap Diff (4)
    BOLD rest (5)
    BOLD faces (6)

Running Dcm2bids
****************
.. note::
    
    Prior to running Dcm2bids for the first time you can optionally run ``dcm2bids_scaffold`` to pre-populate your BIDS
    folder with some key files, like so:

    .. code-block:: bash
        
        dcm2bids_scaffold -o OUTPUT_DIR
    

Once you have written your configuration file, Dcm2bids can be run as follows:

.. code-block:: bash

    dcm2bids -d sourcedata/sub-01 -p 01 -c code/bids_config.json --forceDcm2niix

There's a few arguments to note here:

* ``-d`` refers to the DICOM directory
* ``-p`` refers to participant ID
* ``-c`` refers to the location of your configuration file
* ``--forceDcm2niix`` forces the use of Dcm2niix for the dicom to NIfTI conversion

If this were a multi-session study, you would need to add a session label argument (``-s``) to the command above. For example:

.. code-block:: bash

    dcm2bids -d sourcedata/sub-01 -p 01 -s 02 -c code/bids_config.json --forceDcm2niix

This would convert the data for sub-01, session 02.

Example scripts
***************

Here is an example script that loops through participants to convert dicoms to NIfTI for a single session experiment:

.. code-block:: bash

    #!/bin/bash

    set -e -u

    # You would run this script from the directory you want your BIDS dataset contained in

    for id in `seq -w 1 20` ; do  # seq -w creates a list from 01 to 20
        subj="sub-$id"  # puts "sub-" in front of each id in turn, eg. "sub-01" "sub-02" etc.
        echo "=====> converting $subj..."  # in bash variables are recognised with the $ symbol
        dcm2bids -d sourcedata/$subj -p $id -c code/bids_config.json --forceDcm2niix  # the dcm2bids command
        echo
        echo "Done"
    done


Here is an example script using DataLad to convert either a single session or both sessions for a multi-session experiment:

.. code-block:: bash

    #!/bin/bash

    set -e -u

    echo "Enter subject IDs to add MRI data for: "

    read -a SUBS  # create array from input

    prefix="sub-"

    datalad update -d sourcedata -r --merge
    datalad save -r

    for sub in "${SUBS[@]}"  # loop through array
    do
        label=${sub/#$prefix}  # remove prefix to define participant label
    # Check which session to convert
        read -p "For ${sub}, convert dicoms for session1, session2 or both?
    (Enter session1, session2, or both): " sessn
    # Run conversion
        case "$sessn" in
            session1)  # commands for session1 only
                echo "Converting session 1 only..."
                echo
                datalad run \
                -i sourcedata/${sub}/ses-01/ \
                -o ${sub}/ses-01/ \
                -m "Convert ${sub}/ses-01 to nifti" \
                "dcm2bids -d sourcedata/${sub}/ses-01 -p ${label} -s 01 -c code/bids_config.json --forceDcm2niix" ;;
            session2)  # commands for session2 only
                echo "Converting session 2 only..."
                echo
                datalad run \
                 -i sourcedata/${sub}/ses-02/ \
                 -o ${sub}/ses-02/ \
                 -m "Convert ${sub}/ses-02 to nifti" \
                "dcm2bids -d sourcedata/${sub}/ses-02 -p ${label} -s 02 -c code/bids_config.json --forceDcm2niix" ;;
            both)  # commands for both sessions
                echo "Converting both sessions..."
                echo
                sessions=("01" "02")
                for sesh in "${sessions[@]}"
                do
                    datalad run \
                     -i sourcedata/${sub}/ses-${sesh}/ \
                     -o ${sub}/ses-${sesh}/ \
                    -m "Convert ${sub}/ses-${sesh} to nifti" \
                    "dcm2bids -d sourcedata/${sub}/ses-${sesh} -p ${label} -s ${sesh} -c code/roar_bids_config.json --forceDcm2niix" 
                done ;;
            *)  # else
                    echo "$(tput setaf 1)$(tput bold)ERROR$(tput sgr 0)"  # "ERROR" red & bold
                    echo "Please enter session1, session2, or both" ;;
        esac
    done

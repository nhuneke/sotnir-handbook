.. _intro.rst:

==============================================
Quality Assurance Checks
==============================================
| Contributors: Nathan TM Huneke
| Maintainers: Nathan TM Huneke

------------------------------------------

It is important to check the quality of your fMRI data before embarking on analyses to ensure there are no systematic issues with your data.

Standard deviation and Signal to Noise ratio maps 
--------------------------------------------------

Looking at these maps derived from your functional EPI runs can be helpful for 'eyeballing' 
any clear artefacts or systematic issues with the acquisition of your data.

.. todo::
    Add examples of artefacts on standard deviation and SNR images

Creating standard deviation and tSNR maps
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Some scanners can produce these maps for you, however, you might want to create 
them offline. This can be achieved easily with fslmaths commands. You will need FSL 
to be installed.

.. topic:: The formula for calculating temporal signal to noise (tSNR) is

    tSNR = temporal mean/temporal standard deviation

We can therefore use the following commands to create the maps:

.. code-block:: shell 

    # create mean map
    fslmaths <input_bold.nii.gz> -Tmean <output_mean.nii.gz> 
    
    # create standard deviation map
    fslmaths <input_bold.nii.gz> -Tstd <output_std.nii.gz> 
    
    # calculate temporal SNR (tSNR) 
    fslmaths <output_mean.nii.gz> -div <ouput_std.nii.gz> <output_tSNR.nii.gz> 

Replace the filenames in ``< >`` above with the paths to your input images and chosen output
paths.

Using MRIQC for Quality Assurance
----------------------------------

`MRIQC <https://mriqc.readthedocs.io/en/stable/>`_ is a BIDS app that extracts quality metrics from structural and functional MRI data.

It is best to run and install MRIQC using Docker.

.. note::

    If you are using a university machine then you will need to be given permission to
    use Docker. Please speak to the admin for the machine.

Install MRIQC with Docker
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Type the following to download the latest MRIQC image:

.. code-block:: shell

    docker run -it poldracklab/mriqc:latest --version
    
Run MRIQC with Docker
~~~~~~~~~~~~~~~~~~~~~~

Participant-level
******************

To prevent your machine's RAM from being overloaded, it is best to run 1 participant at a time. Use the following command:

.. code-block:: shell
    
    docker run -it --rm -v \
        <path/to/bids/dataset>:/data:ro -v \
        <desired/path/to/outputs>:/out \
        nipreps/mriqc:latest \
        /data /out participant \
        --participant-label 01 \
        --user $( id -u )
    
.. warning::
    
    The paths above must be *absolute* paths.

If you see potential artifacts on the reports, you can re-run the participant and output extra information:

.. code-block:: shell

    docker run -it --rm -v \
        <path/to/bids/dataset>:/data:ro -v \
        <desired/path/to/outputs>:/out \
        nipreps/mriqc:latest \
        /data /out participant \
        --participant-label 01 \
        --user $( id -u ) \
        --ica --verbose-reports
    
This will provide a more detailed report as well as the results of independent component analysis.

Group-level
************

MRIQC can also generate group-level reports to help you identify any outlying participants. Use the following command to run a group-level QC check:

.. code-block:: shell

    docker run -it --rm -v \
    <path/to/bids/dataset>:/data:ro -v \
    <desired/path/to/outputs>:/out \
    nipreps/mriqc:latest \
    /data /out group \
    --user $( id -u )

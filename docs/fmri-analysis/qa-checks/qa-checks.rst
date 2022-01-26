.. _qa-checks.rst:

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

    tSNR = mean/standard deviation

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

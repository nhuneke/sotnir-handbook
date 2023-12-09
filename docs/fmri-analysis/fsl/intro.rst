.. _intro.rst:

==============================================
fMRI Analysis with FSL
==============================================
| Contributors: Nathan TM Huneke, Mobeen Ali, Yukai Zou
| Maintainers: Nathan TM Huneke

--------------------------------------------

.. note::
    Under construction

FEAT
----

To be added

Viewing FEAT Analyses Results
-----------------------------

In a file browser (e.g. Windows File Explorer), navigate to the output folder of the FEAT analysis. This folder should end with the suffix ``.feat``. Inside this folder, there should be a file called ``report.html``. Double-clicking on this file, a web browser should open and display the status and results of the FEAT analysis, which is a convenient way to view the results. 

While FEAT analysis is still running, it will display "STILL RUNNING" in the main page. When the analysis is complete, open FSLeyes and load the preprocessed fMRI image (``filtered_func_data``) from the ``.feat`` folder. 

FSLeyes: a brief intro
**********************

`FSLeyes <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FSLeyes>`_ is the image viewer released with FSL version ≥ 5.0.10. FSLeyes does not perform any processing or analysis on images.

A complete user guide of FSLeyes can be found `here <https://open.win.ox.ac.uk/pages/fsl/fsleyes/fsleyes/userdoc/>`_. FSLEyes has the following features:

* Orthographic (3 orthogonal slicings) and lightbox (multiple slices) views
* Multiple simultaneous views (orthographic and/or lightbox)
* Timeseries display (via graphs or movie loops)
* Multiple semi-transparent colour-overlays
* Simple freehand image editing (mask drawing)
* 3D rendering

Starting FSLeyes
****************

Basic image viewing
*******************

Unlinking Cursors
*****************

Viewing multiple images
***********************

Viewing Timeseries (4D images)
******************************

Viewing Atlases
***************

FSLeyes - 3D mode
*****************

Brain Extraction Tool (BET)
---------------------------

Accurate brain extraction is crucial for carrying out structural analysis that involves segmentation. In FSL, it is straightforward to perform brain extraction by running BET, but obtaining accurate results will involve some skill and diligence.

For command-line version, you can type ``bet`` to learn about the usage description:

::

    bet <input> <output> [options]

where ``input`` and ``output`` stand for filenames, and ``options`` can be many, or none, of the available extra options. 

Varying the fractional intensity threshold parameter (-f)
**********************************************************

The ``-f`` option in ``bet`` controls the fractional intensity threshold that distinguishes brain from non-brain. By default the value is set on 0.5, and when it is smaller, the brain estimate gets larger. In command line, try setting the ``-f`` option from 0.2 to 0.8, in turn, to see the effect it has. Save these outputs with different names and load them into FSLeyes. 

Troubleshooting Brain Extraction
********************************

The section describes some of the more problematic brain extraction cases, which are common with images that have large FOV and/or substantial bias field.

Using the gradient threshold option (-g)

Dealing with large FOV

1. crop image first to remove the neck
2. provide an estimate of the centre of the brain
3. use other BET options that might be more robust

(Optional) FSLUTILS
-------------------

fslinfo and fslhd
*****************

fslstats
********



fslmaths
********

``fslmaths`` is a very general image calculator and can be used to perform a variety of manipulations of images.

As an example, here we have extracted two images from a functional dataset, ``image0`` and ``image1``. We'd like to calculate the difference between two consecutive timepoint images, which may be used as part of a quality assessment. We will call the output ``imdiff``. To do so, run the following command:

::

    fslmaths image0 -sub image1 imdiff

and view the output (`imdiff`).

Now, to calculate this as a percent difference image, run the following command:

::

    fslmaths imdiff -div image0 -mul 100 imdiffpercent

which will first take the difference image (``imdiff``), divide by the first of the original images (``image0``), multiply by 100, and output ``imdiffpercent``. View the output, and run ``fslstats``.

fslsplit and fslmerge
*********************

fslroi
******

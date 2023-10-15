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

(Optional) Brain Extraction Tool (BET)
--------------------------------------

Troubleshooting Brain Extraction
********************************

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

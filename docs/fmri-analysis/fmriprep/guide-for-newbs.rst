.. _guide-for-newbs.rst:

==============================================
Beginner's Guide to fMRI Pre-processing
==============================================
| Contributors: Nathan TM Huneke, Nick Hedger
| Maintainers: Nathan TM Huneke

---------------------------------------------

Functional neuroimaging aims to relate performance in some sort of task with neural activity in a region of the 
brain.

Logic of fMRI
---------------

The basic logic underlying functional MRI is as follows:
- Firstly, the brain consumes around 20% of our oxygen uptake. This is usually in response to neural activity, which uses up energy and therefore creates a need for oxygen.
- Hemoglobin is a molecule in the blood that can transport this oxygen.
- The magnetic properties of hemoglobin differ depending on whether or not it is carrying oxygen.
- De-oxygenated hemoglobin has what are called paramagnetic properties, which can cause distortions to the local magnetic fields induced by the scanner. 
  This means that protons receive slightly different magnetic field strengths, which interferes with magnetic resonance. 
  By contrast, oxygenated hemoglobin is more diamagnetic and less paramagnetic than de-oxygenated hemoglobin.
- When there is neural activity in a region, metabolic demands increase and so more oxygenated hemoglobin is rushed to the area. 
  As a result, the presence of oxygenated hemoglobin reduces the signal distortions caused by de-oxygenated hemoglobin.

This forms the basis of the blood oxygen level dependent (BOLD) response. 
It is sensible to think of the BOLD response as being the ratio of oxygenated to deoxygenated hemoglobin, which is measured via these distortions to magnetic resonance.

Unlike structural images, where the relative signal intensity in an image depends on the T1 relaxation of the tissue, signal intensity in functional images represents a different, independent component of the MR signal: T2* relaxation. On the application of an RF pulse, 
the precessions of hydrogen protons are aligned in one direction (they are phase coherent), which produces a strong signal. However, immediately afterwards, 
this arrangement is lost and the precessions lose coherence. Spatially proximate spins may interact like bumper cars on a track, causing some spins to 
precess faster than others. This dephasing of precessions leads to an exponential decay in the MR signal that is described by the time constant T2. 
This dephasing can be partly explained by the contribution of paramagnetic artefacts that cause local magnetic field variations, and this contribution is described 
by the time constant T2*. Dephasing in a paramagnetic environment (near deoxygenated hemoglobin) is faster than dephasing in a diamagnetic environment 
(near oxygenated hemoglobin). Thus, pulse sequences sensitive to T2* relaxation show more signal intensity in locations where blood is highly oxygenated.

A Simple Experiment
~~~~~~~~~~~~~~~~~~~~

To clarify,  it is perhaps useful to think of things in terms of a simple experiment (see figure below). Suppose we are interested in recording from the visual cortex, 
which is at the posterior part of the brain. We want to contrast two conditions. In the rest condition (upper row), the observer views a blank screen and in the active condition 
(lower row), the observer views a salient visual stimulus.

In the rest condition, since there is no visual stimulation, there is little neural activity in the visual cortex and so there is a high concentration of deoxy-hemoglobin. 
As a result, the magnetic susceptibility of the nearby protons is distorted and proton dephasing is fast. 
This means that the visual cortex emits a weak T2* signal.

However, in the active condition, the participant views a salient stimulus, this means that there is an increase in neural activity in the visual cortex, and so oxyhemoglobin rushes to this region. 
As a result, there is a reduction in the paramagnetic distortions to magnetic resonance and therefore T2* increases. 
It's this increase in signal that is shown in the image on the right below.

.. figure:: ../images/simple-experiment.png
    :width: 600

    Upon visual stimulation there is an increase in local neural activity in the visual cortex. This results in oxygenated hemoglobin rushing to the area.
    As a result, the paramagnetic distortions to magnetic resonance are reduced and the T2* increases. This is reflected on the image on the right.

|

Components of the BOLD Response
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
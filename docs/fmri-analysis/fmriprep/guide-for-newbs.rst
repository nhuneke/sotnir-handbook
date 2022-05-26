.. _guide-for-newbs.rst:

==============================================
Beginner's Guide to fMRI Preprocessing
==============================================
| Contributors: Nathan TM Huneke, Nick Hedger
| Maintainers: Nathan TM Huneke

---------------------------------------------

Functional neuroimaging aims to relate performance in some sort of task with neural activity in a region of the brain.

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

.. figure:: ../../images/simple-experiment.png
    :width: 600

    Upon visual stimulation there is an increase in local neural activity in the visual cortex. This results in oxygenated hemoglobin rushing to the area.
    As a result, the paramagnetic distortions to magnetic resonance are reduced and the T2* increases. This is reflected on the image on the right.

|

Hemodynamic Response Function
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When we record from a region of neural activity, the BOLD response resembles a hemodynamic response function (HRF). We can explain the shape of this function in 
terms of the concentration of oxygenated and de-oxygenated hemoglobin. 

.. figure:: ../../images/hrf.png
    :width: 600

    Firstly, there tends to be a initial dip in the function, which reflects the neurons consuming oxygen. 
    Therefore temporarily, the concentration of deoxygenated hemoglobin is higher. As a compensatory mechanism, the vascular system rushes more oxygenated hemoglobin 
    to the area, at a faster rate than it can be consumed, giving rise to local blood oxygen levels that are higher than necessary. 
    This results in an elevated response (an overcompensation) that typically peaks after around 6 seconds. The third component is an undershoot. 
    This probably reflects the vascular system tiring, before oxygen consumption returns to normal again, as a result there is temporarily more de-oxyhemoglobin again.

|

The shape of the HRF is not just worth learning about for purely theoretical reasons. It has a number of practical applications. Most notably, the canonical shape of the HRF is an important component 
of the statistical models that are used to analyze functional imaging data.

A Typical Scanning Session
----------------------------

This next section is designed to give you a more tangible idea of what happens during a typical scanning session. 
A typical scanning session consists of at least 3 separate scans. A *localiser scan*, a *high resolution structural scan* and a *functional scan*.

Localiser
~~~~~~~~~~~

Firstly, a  localizer scan is conducted. This consists of a 1-2 minute low resolution scan, that allows the radiographer to localize the brain for further scans. 
The basic idea of this scan is to allow the radiographer to determine where the brain is located in scanner coordinates and use these coordinates to guide further scans.


High Resolution Structural scan
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Next, a high resolution T1 structural scan is collected. Because this is a high resolution image, it takes a long time- usually 8-10 minutes. 
But why, you may ask, are we bothered with collecting a static, structural image for a functional imaging study?

The reason this structural scan is collected is because the functional data that follows is much lower resolution. 
We need this higher resolution scan so that we can register the functional data to an image that has more precise spatial co-ordinates.

By way of illustration, some functional data is plotted in the figure below (a). As you can see, this is very low resolution and it's hard to differentiate 
between structures. In fact, it's hard for us to even tell what part of the brain we are recording from. However, if we superimpose this on the high 
resolution structural scan (b), this all becomes a lot easier. We can see that we are recording from the posterior part of the brain, and we can better 
differentiate between parts of the subjects' anatomy.

.. figure:: ../../images/structural-functional-comparison.png
    :width: 600

    a) Shows low resolution functional data (74*74*36). b) Shows the same data (translucent blue) superimposed on a high resolution image (144*198*200). The functional 
    data has been upsampled and spatially registered to the same space as the high resolution structural data. This registration process improves the ability to make 
    inferences about regions of task-related activation.

|
Functional Scan
~~~~~~~~~~~~~~~~

Next, the functional scan itself is collected. This consists of a series of low-resolution scans, or *volumes* that are collected 
while a task is being performed by the participant. It is important to note that functional data are 4 dimensional. First there is the 3 dimensional image of the 
brain and the fourth dimension is the volume number in the time dimension. Its perhaps useful to think of functional data as being like a 3 dimensional video recording 
of the brain, with each volume being like a 'frame' of a video. Obviously, the length of a functional scan will vary depending on the complexity of 
the particular experimental design and related factors, but a typical functional scan will be around 30 minutes long and is usually broken into a series of 
discrete *functional runs* of approximately 10 minutes.

Functional Scan: Important Parameters
***************************************

There are two parameters of a functional scan that are important to understand. First is the *repetition time*, which is abbreviated to *TR*. This is the length 
of time between successive functional volumes. If the whole brain is scanned, a TR is usually 2-3 seconds. Secondly, there is the *size of the voxels* (resolution), or the 3 dimensional 
units of space that are recorded from. You can think of these in terms of the brain being broken down into as cubes (or more precisely - pyramidal shapes). 
From each voxel there is a corresponding data point. If the voxel size is large, we have a low resolution image, whereas if the voxel size is small the representation 
of space is more precise and the image has higher resolution.

There is an inherent trade off between these two parameters, for instance if we want small voxels, we then have to record more data points per volume 
and thus it takes longer to scan the whole brain. However, if we have large voxels, we only need to record a few data points and thus our TR can be shorter. 
In other words, we can sacrifice spatial resolution for temporal resolution and vice versa. Conceptually, this is the same trade off associated with cathode ray tube (CRT) 
monitors: low resolutions support higher refresh rates than higher resolutions.

Of course, not all functional scans require each volume to be a recording of the entire brain. It is perfectly viable to obtain *partial brain* functional volumes to decrease the 
TR and length of the experiment. In the functional data we saw :ref:`earlier <_guide-for-newbs:High Resolution Structural scan>`, much of the parietal lobe 
was sacrificed so that better spatial resolution of the occipital and temporal lobes could be obtained. 

Functional Scan: Example
*************************

Let's think about some hypothetical functional data for a moment. The main point of this is to illustrate the 4 dimensional nature of the data and the vast amount 
of data handling involved with functional imaging experiments. 

As described above, a functional scan consists of a series of 3 dimensional volumes, each of which is composed of voxels. A typical voxel might be 
*3mm cubed* in size. To scan an entire human brain once, *33 separate slices* may be required, each containing a 64*64 grid of voxels. Per individual volume, 
we are therefore recording *135,168* data points. However, we don't just obtain one volume in a functional scan, we record very many successively. 
In a 30 minute functional scan with a TR of 2 seconds, each of these 135,168 data points would need to be recorded *900* separate times. 
This gives us a total of *121,651,200 data points*. Thus, even making fairly standard assumptions about parameters, the amount of data involved in functional 
imaging is somewhat intimidating.

.. figure:: ../../images/example-4d.png
    :width: 600

    A functional run is composed of successive volumes, each of which contains slices. It is intuitive to think of functional data like a 3D video recording 
    of the brain.

|
Other Scans: Shimming and Field Map 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Under optimal conditions, a scanner would have an entirely uniform magnetic field. Even if this were possible, we unfortunately have to place humans inside of 
the scanner, which distorts the magnetic field. Two scans are occasionally conducted to characterise and partially correct for this distortion. 
After the participant enters the scanner, all inhomogeneities can be corrected via a process known as *shimming*. Often however, these distortions 
will eventually reappear and it is impractical and time consuming to keep repeating this process. As a result, a *field map scan* is often collected to 
characterise the inhomogeneity in the magnetic field, so that it can later be corrected in data preprocessing.


.. _intro.rst:

==============================================
Diffusion Tensor Imaging: An Introduction
==============================================
| Contributors: Yukai Zou
| Maintainers: Yukai Zou

------------------------------------------

What is Diffusion Tensor Imaging (DTI)?
***************************************

Diffusion imaging is a Magnetic Resonance Imaging (MRI) technique that quantitatively monitors the thermal (Brownian) motion of water molecules. In the human brain, water molecules occupy most of the tissue, and water protons contribute to most of the signals in MRI [Chanraud2010]_. Diffusion imaging **measures** the microstructural integrity of white matter, both non-invasively and quantitatively, through measuring the magnitude, anisotropy, and directionality of water diffusion via a *tensor* model of diffusion [Mukherjee2008a]_. The tensor is composed of three *eigenvectors*, and each eigenvector characterizes the diffusion in one of the three dimensions [Chanraud2010]_. The lengths of the three axes are defined as *eigenvalues* ($\lambda_1, \lambda_2, \lambda_3$). Mean diffusivity (MD) and fractional anisotropy (FA) can be **analysed** from the three eigenvalues for each voxel of the diffusion image:

.. math::

    \textrm{MD} = \frac{\lambda_1 + \lambda_2 + \lambda_3}{3}

.. math::

    \textrm{FA} = \sqrt{\frac{(\lambda_1-\textrm{MD})^2 + (\lambda_2-\textrm{MD})^2 + (\lambda_3-\textrm{MD})^2}{2(\lambda_1^2 + \lambda_2^2 + \lambda_3^2)}}

MD, a.k.a. Apparent Diffusion Coefficient (ADC), represents cellular density and extracellular volume, whereas FA is a scalar value ranging from 0 (isotropic) to 1 (anisotropic) representing the diameter, density, and the complexity of the axonal network [Beaulieu2002]_. Voxels with low FA and high MD values indicate less directionality of water diffusion, which may be due to demyelination or disorganized axonal structures [Pfefferbaum2005]_. 

DTI-based Tractography
**********************

Based on the tensor modeling, fiber tractography is an algorithm for reconstructing the trajectory of white matter fibers [Mukherjee2008a]_, which is a powerful tool for **analyzing** *structural connectivity* between different brain regions [Jbabdi2015]_. The theoretic underpinning is that in each voxel (single unit of a volumetric image), the dominant orientation of white matter fiber is assumed to follow the *primary eigenvector* of the diffusion tensor [Mukherjee2008a]_.

Advantages
**********

There are several advantages for diffusion imaging and tractography. First, compared to conventional (T1- and T2-weighted) MRI techniques, diffusion imaging and tractography shows *more detailed information of the brain*, including white matter microstructure and neuronal pathways, which cannot be achieved under the spatial resolution of conventional MRI. This information can assist doctors to evaluate the recovery time of patients from brain injury, as well as allow researchers to better understand mechanisms of complex neuropathological disorders, such as sports-related concussion and traumatic brain injury. Second, compared to invasive histological methods, diffusion imaging and tractography is *noninvasive*, allowing reconstruction of neuronal pathways without the need of sacrificing subjects or any chemical staining. Third, compared to X-ray computed tomography (CT), there is *no radiation* associated with diffusion imaging and tractography, which allows subjects to be monitored at multiple time points without the concern of tissue damage from too much radiation exposure.

Limitations
***********

Currently, the limitations of diffusion imaging and tractography are:
    
1.  The spatial resolution is relatively low. To investigate an anatomical region or map a specific neuronal pathway, diffusion images and fiber tracts often need to combine with anatomical MR scans at higher resolution. In order to achieve higher spatial resolution and resolve white matter tracts that are relatively small, the acquisition time needs to be longer, which is a **technical barrier** in signal sampling [Mukherjee2008b]_;

2.  Although fiber trajectory can be reconstructed, the modeled diffusion has antipodal symmetry, meaning that the model fails to delineate whether a neuronal pathway is anterograde or retrograde \cite[Mukherjee2008a]_; therefore, advanced modeling methodology needs to address this **technical barrier** to provide richer physiological insights of fibers;

3.  Diffusion imaging and tractography is prone to the assumptions in tensor modeling to characterize axonal pathways. Crossing fibers (e.g. joint between corpus callosum and corona radiation, medial fiber bundle and anterior thalamic radiation, fornix and striatal terminalis, etc.) violate the assumption of a simple tensor model and cannot be resolved [Thomas2014]_. To overcome this **technical barrier**, advanced diffusion imaging techniques, such as high angular resolution diffusion imaging [Tuch2002], have been developed to better delineate orientations of crossing fiber [Hess2007]_.

Overall, it is important to be aware of the limitations and technical barriers of diffusion imaging and tractography, as unawareness or ignorance can lead to systematic errors, complicated interpretations, or even false discoveries.

Relevant Readings
*****************

- `What is Diffusion <https://mri-q.com/what-is-diffusion.html>`_
- `What is Apparent Diffusion Coefficient (ADC) <https://mriquestions.com/apparent-diffusion.html>`_
- `How do you make a Diffusion Weighted Image <https://mriquestions.com/making-a-dw-image.html>`_
- `Trace versus ADC <https://mriquestions.com/trace-vs-adc-map.html>`_

.. topic:: References

    .. [Chanraud2010] Chanraud S, Zahr N, Sullivan EV, Pfefferbaum A, “MR diffusion tensor imaging: A window into white matter integrity of the working brain,” 2010. doi: `10.1007/s11065-010-9129-7 <https://doi.org/10.1007/s11065-010-9129-7>`_.

    .. [Mukherjee2008a] Mukherjee P, Berman JI, Chung SW, Hess CP, Henry RG, “Diffusion tensor MR imaging and fiber tractography: Theoretic underpinnings,” 2008. doi: `10.3174/ajnr.A1051 <https://doi.org/10.3174/ajnr.A1051>`_.

    .. [Mukherjee2008b] Mukherjee P, Chung SW, Berman JI, Hess CP, Henry RG, “Diffusion tensor MR imaging and fiber tractography: Technical considerations,” in American Journal of Neuroradiology, 2008. doi: `10.3174/ajnr.A1052 <https://doi.org/10.3174/ajnr.A1052>`_.

    .. [Pfefferbaum2005] Pfefferbaum A and Sullivan EV, “Disruption of brain white matter microstructure by excessive intracellular and extracellular fluid in alcoholism: Evidence from diffusion tensor imaging,” Neuropsychopharmacology, 2005. doi: `10.1038/sj.npp.1300623 <https://doi.org/10.1038/sj.npp.1300623>`_.

    .. [Jbabdi2015] Jbabdi S, Sotiropoulos SN, Haber SN, Van Essen DC, Behrens TE, “Measuring macroscopic brain connec- tions in vivo,” 2015. doi: `10.1038/nn.4134 <https://doi.org/10.1038/nn.4134>`_.

    .. [Beaulieu2002] Beaulieu C, “The basis of anisotropic water diffusion in the nervous system - a technical review,” NMR Biomed, vol. 15, no. 7-8, pp. 435–455, 2002. doi: `10.1002/nbm.782 <https://doi.org/10.1002/nbm.782>`_.

    .. [Thomas2014] Thomas C, Ye FQ, Irfanoglu MO, Modi P, Saleem KS, Leopold DA, Pierpaoli C, “Anatomical accuracy of brain connections derived from diffusion MRI tractography is inherently limited,” Proceedings of the National Academy of Sciences, 2014. doi: `10.1073/pnas.1405672111 <https://doi.org/10.1073/pnas.1405672111>`_.

    .. [Tuch2002] Tuch DS, Reese TG, Wiegell MR, Makris N, Belliveau JW, Wedeen VJ, “High angular resolution diffusion imaging reveals intravoxel white matter fiber heterogeneity,” Magnetic Resonance in Medicine, 2002. doi: `10.1002/mrm.10268 <https://doi.org/10.1002/mrm.10268>`_.

    .. [Hess2007] Hess CP and Mukherjee P, “Visualizing White Matter Pathways in the Living Human Brain: Diffusion Tensor Imaging and Beyond,” 2007. doi: `10.1016/j.nic.2007.07.002 <https://doi.org/10.1016/j.nic.2007.07.002>`_.
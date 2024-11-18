.. _intro.rst:

==============================================
eXtensible Neuroimaging Archive Toolkit (XNAT)
==============================================
| Contributors: Yukai Zou
| Maintainer: Yukai Zou

.. important::
   
   Please contact Scientific Computing in UHS Imaging Physics (scicom@uhs.nhs.uk) with any queries.

What is XNAT?
--------------------

XNAT_ stands for eXtensible Neuroimaging Archive Toolkit. It is an open-source imaging informatics platform that can store, manage, and share neuroimaging data. Originally developed by the Buckner Lab (now at Harvard University) and the `Neuroinformatics Research Group<https://github.com/NrgXnat>`_ at Washington University in St Louis, XNAT facilitates common management, productivity, and quality assurance tasks for imaging and associated data. Thanks to its extensibility, XNAT has widely implemented to support a wide range of imaging-based projects around the world.

.. `XNAT: <https://www.xnat.org/>`_


How has XNAT been implemented at UHS?
-----------------------------------------------------------

The XNAT services are at the following addresses:

=============  =================  =======================
  Instances                 Use Cases                    Urls
=============  =================  =======================
Identifiable   UHS internal only  UHS_XNAT_IDENTIFIABLE_
Pseudonymised  UHS internal only  UHS_XNAT_ANON_
De-identified  UHS external*      https://xnat.uhs.nhs.uk
=============  =================  =======================
* Currently under maintenance

.. `UHS_XNAT_IDENTIFIABLE<https://connect.uhs.nhs.uk/app/template/,DanaInfo=rhmxnat.uhs.nhs.uk+Login.vm#!>`_
.. `UHS_XNAT_ANON<https://connect.uhs.nhs.uk/app/template/,DanaInfo=rhmxnatanon.uhs.nhs.uk+Login.vm#!>`_

Anonymisation
--------------------

XNAT has built-in anonymisation/pseudonymisation using ``DicomEdit`` scripts, but users can consider using customised script such as ``pydicom`` to include important capabilities. ``DicomEdit`` is a domain-specific mini language that was developed by the same team as XNAT and is documented at `XNAT Tools: DicomEdit 6.2 Language Reference`_. Updated version of ``DicomEdit`` may have built-in important capabilities, e.g., replacing UIDs with new UIDs in a coherent way that does not break referential integrity, but this is not guaranteed.

.. `XNAT Tools: DicomEdit 6.2 Language Reference<https://wiki.xnat.org/xnat-tools/dicomedit/dicomedit-6-2-language-reference>`_

Download Data from XNAT
------------------------------------

XNAT makes the individual slices available at a fixed URL for download, rather it has a `REST API`_ that is accessible via URLs and allows programmatic `discovery & downloading`_ of those projects, **sessions**, and images that the user has access to. It implements access control using logon sessions, so all XNAT users have an account that they can log in to, and each XNAT **project** (the top-level object in XNAT’s hierarchy, a project contains both subjects/patients and scans) has access control lists that grant specific users a given level of access.

Where to put the data
~~~~~~~~~~~~~~~~~~~~~

The Python library for that API should enable downloads to research filestore or local storage (if required). It is possible to download directly to the scratch space on Iridis, if running on a node that can access both the scratch space and the XNAT API.

 - Read ? for more information on research filestore & mapping network drive protocols

.. _`REST API`: https://wiki.xnat.org/display/XAPI/XNAT+API+Documentation
.. _`discovery & downloading`: https://wiki.xnat.org/display/XAPI/How+To+Download+Files+via+the+XNAT+REST+API

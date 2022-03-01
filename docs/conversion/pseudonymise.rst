.. _pseudonymise.rst:

=========================================
Pseudonymise your dataset
=========================================
| Contributors: Nathan TM Huneke
| Maintainers: Nathan TM Huneke

------------------------------------------

If you plan to share your dataset then it is important to pseudonymise/anonymise your
dataset in line with data protection laws. You should ensure JSON sidecar files do not
include identifiable information and that anatomical images have facial structures removed.

It is best to store pseudonymised data in a separate dataset from the source identifiable data.
The reason for this is if you are using version control such as DataLad then it might be possible
to retrieve identifiable information from the version history.

Removing facial structures with PyDeface 
--------------------------------------------------

`PyDeface <https://github.com/poldracklab/pydeface>`_ is a BIDS app that allows easy 
removal of facial structures from anatomical MRI scans. 

Install PyDeface
~~~~~~~~~~~~~~~~~

Install with::

    pip install pydeface

How to use PyDeface
~~~~~~~~~~~~~~~~~~~~~

Assuming you will be storing pseudonymised data in a new dataset, you can use the following command::

    pydeface \
    --outfile pseudonymised_dataset/path/to/T1w.nii.gz \
    --force \
    sourcedata/path/to/T1w.nii.gz

The ``--outfile`` argument specifies the output path. The ``--force`` argument will overwrite
the output if it already exists. It is useful to leave this on to prevent errors. Finally, 
the path to the original anatomic image is the only positional argument required.

Pseudonymisation with BIDSonym
--------------------------------------------------

.. todo::
    Add info re: BIDSonym


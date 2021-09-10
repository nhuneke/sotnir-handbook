.. _datalad.rst:

==============================================
A Brief Introduction to DataLad
==============================================
| Contributors: Nathan TM Huneke
| Maintainers: Nathan TM Huneke

------------------------------------------

The following text is adapted from the `DataLad handbook <http://handbook.datalad.org/en/latest/basics/101-180-FAQ.html#dataset-textblock>`_.

`DataLad <https://www.datalad.org>`_ is a free and open source command line tool, available for all
major operating systems, and builds up on Git and `git-annex
<https://git-annex.branchable.com>`__ to allow sharing, synchronizing, and
version controlling collections of large files in repositories known as DataLad datasets. You can find information on
how to install DataLad at `handbook.datalad.org/en/latest/intro/installation.html
<http://handbook.datalad.org/en/latest/intro/installation.html>`_.

Get the dataset
^^^^^^^^^^^^^^^

A DataLad dataset can be ``cloned`` by running::

   datalad clone <url>

Once a dataset is cloned, it is a light-weight directory on your local machine.
At this point, it contains only small metadata and information on the
identity of the files in the dataset, but not actual *content* of the
(sometimes large) data files.

Retrieve dataset content
^^^^^^^^^^^^^^^^^^^^^^^^

After cloning a dataset, you can retrieve file contents by running::

   datalad get <path/to/directory/or/file>

This command will trigger a download of the files, directories, or
subdatasets you have specified.

DataLad datasets can contain other datasets, so called *subdatasets*. If you
clone the top-level dataset, subdatasets do not yet contain metadata and
information on the identity of files, but appear to be empty directories. In
order to retrieve file availability metadata in subdatasets, run::

   datalad get -n <path/to/subdataset>

Afterwards, you can browse the retrieved metadata to find out about
subdataset contents, and retrieve individual files with ``datalad get``. If you
use ``datalad get <path/to/subdataset>``, all contents of the subdataset will
be downloaded at once.

Stay up-to-date
^^^^^^^^^^^^^^^

DataLad datasets can be updated. The command ``datalad update`` will *fetch*
updates and store them on a different branch (by default
``remotes/origin/master``). Running::

   datalad update --merge

will *pull* available updates and integrate them in one go.

Find out what has been done
^^^^^^^^^^^^^^^^^^^^^^^^^^^

DataLad datasets contain their history in the ``git log``.
By running ``git log`` (or a tool that displays Git history) in the dataset or on
specific files, you can find out what has been done to the dataset or to individual files
by whom, and when.

Saving changes you make to a dataset
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you make a change to a dataset, you will need to save it into the history 
so that you or other users in the future can see what was done when and by whom. The
command ``datalad status`` will show you whether any changes need to be saved. If you run
this command you might see either the message::

    nothing to save, working tree clean

In which case the log is up to date, or::

    modified: file1.txt (file)

There is a file (``file1.txt``) that has been modified. This modification needs to be
saved in the dataset's history. To do so run a ``datalad save`` command. This will
produce the following output::

    add(ok): file1.txt (file)                                                       
    save(ok): . (dataset)                                                           
    action summary:                                                                 
        add (ok: 1)
        save (ok: 1)

``file1.txt`` was added to the repository and then the dataset was saved. It is
useful to add a message regarding what was saved, so that you can keep track of 
what has been done to the dataset. To do so use the ``-m`` argument, e.g.:

.. code-block:: bash

    datalad save -m "Add file1.txt"

If you now look at the ``git log`` you will see that this entry is accompanied by the 
message that file1.txt was added::

    commit 7a286d45195b7ac6a167fefb2a2229fa87af2425
    Author: nh6g15 <n.huneke@soton.ac.uk>
    Date:   Mon Jun 21 14:49:43 2021 +0100

        Add file1.txt

    commit a736983ec90a2094ce401105173122f9a9033824
    Author: nh6g15 <n.huneke@soton.ac.uk>
    Date:   Thu Jun 17 14:34:17 2021 +0100

        Apply YODA dataset setup

    commit 8bf3c337ef7c06852ffe07ee738eae7f44b1f46c
    Author: nh6g15 <n.huneke@soton.ac.uk>
    Date:   Thu Jun 17 14:34:15 2021 +0100

        [DATALAD] new dataset

DataLad Run
^^^^^^^^^^^^

Possibly the most useful feature of DataLad for computationally intensive analyses (e.g. neuroimaging) 
is the ``datalad run`` command. Using this command allows you to capture your command(s), fetch relevant files, 
do something with them, and then save the results. 

For example, the following ``datalad run`` command, runs a script on a file called 
``anonymised_dataset.csv`` to convert it to long format:

.. code-block:: bash

    datalad run \
        -m "Save long format dataset" \
        -i anonymised_dataset.csv \
        -o dataset_long_format.csv \
        "code/convert2long.R"

After running this, checking the ``git log`` will show the following::

    commit 1eac06986726b3f98c61b0b7eab0964ca54c2e0b (HEAD -> master)
    Author: nh6g15 <n.huneke@soton.ac.uk>
    Date:   Fri Jun 25 16:17:16 2021 +0100

        [DATALAD RUNCMD] Save long format dataset
        
        === Do not change lines below ===
        {
        "chain": [],
        "cmd": "code/convert2long.R",
        "dsid": "9663676d-5ac4-4071-9406-6ee778f7d49e",
        "exit": 0,
        "extra_inputs": [],
        "inputs": [
        "anonymised_dataset.csv"
        ],
        "outputs": [
        "dataset_long_format.csv"
        ],
        "pwd": "."
        }
        ^^^ Do not change lines above ^^^

Because the command and files needed are all saved in the log, we can even re-run this command if needed! 
To do so, we use ``datalad rerun <SHASUM>`` using the SHASUM of the commit in question. For example:

.. code-block:: bash

    datalad rerun 1eac06986726b3f98c61b0b7eab0964ca54c2e0b

I strongly suggest you read the Chapter on ``datalad run`` in the `DataLad handbook <http://handbook.datalad.org/en/latest/basics/basics-run.html>`_ 
as this command is so important.

.. note:: 
    
    To add: 

    - Using DataLad with GitLab
    - Remote Indexed Archives for dataset storage and backup

More information
^^^^^^^^^^^^^^^^

More information on DataLad and how to use it can be found in the DataLad Handbook at
`handbook.datalad.org <http://handbook.datalad.org/en/latest/index.html>`_. The chapter
`What you really need to know <http://handbook.datalad.org/en/latest/intro/executive_summary.html#>`_ 
is particularly useful.
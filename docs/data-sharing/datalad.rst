.. _datalad.rst:

==============================================
DataLad: Distributed Data Management
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

.. note:: 

    If you are using my :ref:`neuroimaging conda environment <getting-started/linux-machines:3. create a conda environment for your software and analyses>` then datalad will be installed.

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

Dataset Storage and Backup
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

DataLad includes tools for easily managing dataset storage and backup. These work very nicely with the 
University's research filestore. A suggested workflow is described below.

DataLad Siblings
------------------

Before understanding how DataLad can be used for storage and backup, it is important to understand the 
concept of a `DataLad sibling <http://handbook.datalad.org/en/latest/basics/101-121-siblings.html>`_.
A datalad sibling is essentially a 'copy' of a dataset stored in another location. Each sibling will 
have its own ``git log``, and changes made in either dataset can be incorporated into the other with a 
``datalad update`` command. For dataset storage and backup, we will be using a special kind of sibling 
known as a ``special remote``. We will use two types of ``special remote``: ``remote indexed archives`` and a 
``gitlab remote``.

Remote Indexed Archives
------------------------

`RIA stores <http://handbook.datalad.org/en/latest/beyond_basics/101-147-riastores.html#>`_ can be easily created or extended from within any dataset. 
The advantage of using an RIA store is that the remote machine does not need datalad to be installed. Nevertheless, 
datalad will still be able to find and retrieve dataset contents through a ``datalad get`` command. The RIA 
store is therefore perfect for content storage and backup, particularly as the University filestore is regularly 
backed up itself.

The RIA store is created with the following command::

    datalad create-sibling-ria -s ria-backup ria+<URL>

If using the university filestore you would replace ``<URL>`` with the path to access your research filestore via 
SSH. This takes the following form::

    ssh://ssh.soton.ac.uk:/research/absolute/path/to/ria-store

The final command therefore looks like this::

    datalad create-sibling-ria -s ria-backup ria+ssh://ssh.soton.ac.uk:/research/absolute/path/to/ria-store

.. note:: 

    To access your research filestore via SSH you need to ask iSolutions for the directory to be 
    ``NFS`` and you need to be added to the list of ``SSH gateway users``.

To backup your dataset contents in the RIA store, use the following command::

    datalad push --to ria-backup

.. tip:: **Accessing a directory via SSH without password**

    It can be useful to set up access to your filestore via SSH without the need for a 
    password. This way you can automate operations like getting dataset contents or pushing 
    dataset updates without needing to input your password every 5 seconds. Doing this 
    is very straightforward through the use of an ``SSH key``.

    First on your machine, type the following command::

        ssh-keygen

    Just use the defaults when prompted by pressing return. Next, copy your key to the 
    SSH server with::

        ssh-copy-id user@server

    You should now be able to login without using a password. 
    
    This key can be copied (using secure copy) to 
    any other machine to allow access to the same server without using a password::

        scp ~/.ssh/id_<key> user@machine:~/.ssh/id_<key>
        scp ~/.ssh/id_<key>.pub user@machine:~/.ssh/id<key>.pub

GitLab Siblings
----------------

RIA stores are great, but they have one problem: *they are not human-readable*. Here is 
an example of what an RIA store actually looks like::

     /path/to/my_riastore
    ├── 946
    │   └── e8cac-432b-11ea-aac8-f0d5bf7b5561
    │       ├── annex
    │       │   └── objects
    │       │       ├── 6q
    │       │       │   └── mZ
    │       │       │       └── MD5E-s93567133--7c93fc5d0b5f197ae8a02e5a89954bc8.nii.gz
    │       │       │           └── MD5E-s93567133--7c93fc5d0b5f197ae8a02e5a89954bc8.nii.gz
    │       │       ├── 6v
    │       │       │   └── zK
    │       │       │       └── MD5E-s2043924480--47718be3b53037499a325cf1d402b2be.nii.gz
    │       │       │           └── MD5E-s2043924480--47718be3b53037499a325cf1d402b2be.nii.gz
    │       │       ├── [...]
    │       │       └── [...]
    │       ├── archives
    │       │   └── archive.7z
    │       ├── branches
    │       ├── config
    │       ├── description
    │       ├── HEAD
    │       ├── hooks
    │       │   ├── applypatch-msg.sample
    │       │   ├── [...]
    │       │   └── update.sample
    │       ├── info
    │       │   └── exclude
    │       ├── objects
    │       │   ├── 05
    │       │   │   └── 3d25959223e8173497fa7f747442b72c31671c
    │       │   ├── 0b
    │       │   │   └── 8d0edbf8b042998dfeb185fa2236d25dd80cf9
    │       │   ├── [...]
    │       │   │   └── [...]
    │       │   ├── info
    │       │   └── pack
    │       ├── refs
    │       │   ├── heads
    │       │   │   ├── git-annex
    │       │   │   └── master
    │       │   └── tags
    │       ├── ria-layout-version
    │       └── ria-remote-ebce196a-b057-4c96-81dc-7656ea876234
    │           └── transfer
    ├── error_logs
    └── ria-layout-version

Cloning this dataset would involve finding out the ``dataset id``, which is not trivial 
when you don't know where to look. Instead, we can store a human-readable version of the dataset 
on the University's `GitLab instance <https://git.soton.ac.uk>`_. GitLab is not suitable for storing
dataset contents (other than code), so does need to be used in conjunction with the filestore. GitLab instead 
stores metadata about the dataset, allowing retrieval of contents from the RIA store using 
human-readable commands. This is very useful when collaborating with others on a project.

Setup 
*******

Before a GitLab remote can be created, you need to complete a few setup steps:

1. Generate a personal access token for GitLab `here <(https://git.soton.ac.uk/-/profile/personal_access_tokens)>`_. 
2. Copy and paste the following into a text file, inserting your personal access token in the appropriate field::

    [soton] 
    url = https://git.soton.ac.uk
    private_token = [insert token here]

3. Save this file in your ``home`` directory (``~``) as ``.python-gitlab.cfg``.

Create the GitLab remote
**************************

To create a GitLab remote, use the following command::

    datalad create-sibling-gitlab -s gitlab --site soton --project <path/to/project>

The metadata and code can then be pushed to gitlab with::

    datalad push --to gitlab

Human-readable metadata will now be visible at ``https://git.soton.ac.uk/path/to/project``. 
The dataset can then be ``cloned`` with::

    datalad clone https://git.soton.ac.uk/path/to/project .

assuming the cloner has permissions to view the dataset. Contents can then be retrieved with a 
``datalad get`` as datalad will by default search the RIA store for contents.

.. note:: 

    To reduce complexity, it helps to create a GitLab remote for the ``superdataset`` **only**. 
    Any subdatasets can be backed up to an RIA store. As long as the superdataset is cloned, it is 
    possible to then retrieve subdataset contents from the RIA store. One line of code needs to be run 
    in the superdataset to configure this::

       git config -f .datalad/config "datalad.get.subdataset-source-candidate-origin" "ria+<URL>#{id}" 

Procedures for Setting Up Datasets 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To help speed up the process of setting up a new datalad dataset (including backup siblings), 
I have written a number of `procedures <http://handbook.datalad.org/en/latest/basics/101-124-procedures.html>`_.
The github repository including installation and usage instructions is `here <https://github.com/nhuneke/dataset-setup-procedures>`_.

More information
^^^^^^^^^^^^^^^^

More information on DataLad and how to use it can be found in the DataLad Handbook at
`handbook.datalad.org <http://handbook.datalad.org/en/latest/index.html>`_. The chapter
`What you really need to know <http://handbook.datalad.org/en/latest/intro/executive_summary.html#>`_ 
is particularly useful.

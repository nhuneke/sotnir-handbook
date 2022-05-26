.. _unix-basics:

============
Unix Basics
============
| Contributors: Nathan TM Huneke, Harry Fagan, Yukai Zou
| Maintainers: Nathan TM Huneke
------------------------

Unix
------
* Unix is an operating system (like Mac or Windows).
* It uses a command line interface (or command line) where you type commands you want to run into a terminal.
* Command line interpreters are called shells (two commonly used ones are bash [Bourne-again shell] and zsh [Z-shell])
* Most neuroimaging packages need to be run from a command line
* Mac and Linux have Terminals installed. Windows users need to install a Terminal emulator to use Unix commands. We do not recommend attempting neuroimaging analyses on a Windows machine. 

.. note::
    You can practice using Unix online with JupyterLab (see https://neuroimaging-core-docs.readthedocs.io/en/latest/pages/unix.html for an excellent tutorial).
    
    An excellent tutorial on the use of the Unix Shell is available `here <https://swcarpentry.github.io/shell-novice/>`_.

Basic Unix Commands
--------------------

- ``pwd`` Print Working Directory, tells you the current directory you are in  
- ``cd directory``    Change Directory, takes to you the directory specified                                                                        
- ``cd ~``               Go to home directory                                                                                                           
- ``cd /``                 Go to root directory                                                                                                         
- ``ls``                    List, lists the contents of the directory you are in                                                                        
- ``ls <directory>`` lists contents of the specified directory                                                                                           
- ``ls -a``                lists all files and directories in the directory you are in (including hidden ones which start with an “.” and don’t appear is you just you the “ls” command)
- ``ls -l``                 Long list, lists all files and directory with ownership and user permissions                                        
- ``ls -al``               Long list (including hidden files and directories)                                                                         
- ``mkdir <name>``  creates a directory with that name                                                                                                   
- ``mkdir .<name>`` creates a hidden directory with that name                                                                                         
- ``history``            lists all recently run commands                                                                                                
- ``!<number>``   re-runs command specified (by number from history list)                                                                     
- ``cp -r <from> <to>`` copies a directory from one path to another path                                                                           
- ``mv <from> <to>``  renames a file or directory                                                                                                         
- ``rm <file>``      deletes a file                                                                                                               
- ``rm -rf <directory>`` deletes a directory                                                                                                             

Important Unix Directories
--------------------------

- ``/bin``               Where built-in Unix commands (e.g. ``ls``, ``mkdir``, etc...) are stored.                                              
- ``/etc``               Where system profiles are stored (e.g. users and passwords).                                                      
- ``/usr/local/bin`` Where user-installed programmes are often stored, unless user specifies a different install location

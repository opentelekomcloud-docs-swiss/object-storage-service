:original_name: obs_03_1060.html

.. _obs_03_1060:

Creating a Folder
=================

Create a folder on OBS Browser+.

Context
-------

Unlike a file system, OBS does not involve the concepts of file and folder. For easy data management, OBS allows you to simulate a folder by adding a slash (/) to the name of an object.

Procedure
---------

#. Log in to OBS Browser+.
#. Click the bucket where you want to create a folder and click **Create Folder**.
#. In the displayed dialog box, enter a folder name and click **OK**.

   -  A folder name cannot contain the following special characters: ``\:*?'<>|``
   -  A folder name cannot start or end with a period (.) or slash (/).
   -  A folder name cannot exceed 1,023 bytes. The length of a folder name is the sum of the length of its own name and the length of its upper-level directory names. The total length cannot exceed 1,023 bytes. Directories of different levels are automatically separated by slashes (/). For example, if the upper-level directory of **folder01** is **folder02**, the name length of folder **folder01** is the length of **folder02/folder01/**.
   -  A single slash (/) separates and creates multiple levels of folders.

#. Click **OK**.

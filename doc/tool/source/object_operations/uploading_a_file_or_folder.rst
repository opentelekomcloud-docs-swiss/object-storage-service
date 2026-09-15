:original_name: obs_03_1061.html

.. _obs_03_1061:

Uploading a File or Folder
==========================

Upload local files or folders to OBS. If you do not specify a storage class during file or folder upload, any file or folder you upload will inherit the storage class of the bucket by default.

Context
-------

Files are uploaded using multipart upload on OBS Browser+. With multipart upload, you can upload a single file with the maximum size of 48.8 TB.

A file or folder name cannot exceed 1,023 bytes. The length of a file name is the sum of the length of its own name and the length of its upper-level directory names. The total length cannot exceed 1,023 bytes. Directories of different levels are automatically separated by slashes (/). For example, if the upper-level folder of file **file01** is **folder01**, the name length of file **file01** is the length of **folder01/file01**.

Prerequisites
-------------

Before uploading a file or folder, you have :ref:`downloaded <obs_03_1003>` and :ref:`installed <obs_03_1005>` OBS Browser+.

Procedure
---------

#. Log in to OBS Browser+.

#. Click the bucket where you want to upload files or folders.

#. Click **Upload** and then **Add File** or **Folder**.

   For better experience when using the **Add File** function, you are advised to upload a maximum of 100 files at a time. If you need to upload more, place all the files in a folder and upload them by adding a folder.

   .. caution::

      You must have access to the file you want to upload, or the file upload will fail.

#. In the displayed dialog box, select the file or folder you want to upload and click **Open**.

   You can upload one folder or multiple files at a time. To upload multiple files, hold down **Ctrl** or **Shift** to select multiple files and batch upload them. You can also press **Ctrl+A** to select all files. The operations are consistent with those in Windows operating systems.

#. Click **OK**.

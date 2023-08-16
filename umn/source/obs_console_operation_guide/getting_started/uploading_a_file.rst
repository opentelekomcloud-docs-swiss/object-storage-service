:original_name: obs_03_0307.html

.. _obs_03_0307:

Uploading a File
================

This section describes how to upload local files to OBS over the Internet. These files can be texts, images, videos, or any other type of files.

.. note::

   You can upload a file of up to 50 MB using OBS Console.

   If versioning is disabled and the name of a newly uploaded file is the same as that of a file in the bucket, the newly uploaded file automatically overwrites the existing file and does not retain the ACL information of the existing file. If the name of the newly uploaded folder is the same as that of a folder in the bucket, the two folders will be merged, and files in the new folder will overwrite namesake files in the old folder.

   If versioning is enabled and the name of a newly uploaded file is the same as that of a file in the bucket, a new version is added to the existing file. For details about versioning, see :ref:`Versioning Overview <en-us_topic_0045853504>`.

Prerequisites
-------------

-  At least one bucket has been created.
-  If you want to classify files, you can create folders and upload files to different folders. For details about how to create a folder, see :ref:`Creating a Folder <obs_03_0316>`

Procedure
---------

#. In the bucket list, click the bucket to be operated. The **Overview** page of the bucket is displayed.

#. In the navigation pane, click **Objects**.

#. Go to the folder to which objects are uploaded. Click **Upload Object**. The **Upload Object** dialog box is displayed.

   .. note::

      If the files that you want to upload to OBS are stored in Microsoft OneDrive, it is recommended that the names of these files contain a maximum of 32 characters.


   .. figure:: /_static/images/en-us_image_0000001180660152.png
      :alt: **Figure 1** Uploading objects

      **Figure 1** Uploading objects

#. Click **Select File** to open the local file browser dialog box.

#. Select the file that you want to upload and click **Open**.

#. Click **Upload**.

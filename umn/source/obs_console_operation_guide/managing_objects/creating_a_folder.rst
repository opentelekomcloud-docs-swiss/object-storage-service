:original_name: obs_03_0316.html

.. _obs_03_0316:

Creating a Folder
=================

You can create folders in a bucket on OBS Console to help organize and manage your data more efficiently.

Background Information
----------------------

-  Unlike a file system, OBS does not involve the concepts of file and folder. For easy data management, OBS provides a method to simulate folders. In OBS, an object is simulated as a folder by adding a slash (/) to the end of the object name on OBS Console. If a path ends with a slash (/), it indicates that the object is a folder. The hierarchical depth of the object does not affect the performance of accessing the object.
-  OBS Console does not support the download of folders. You can use OBS Browser to download folders.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.
#. Click **Create Folder**, or click a folder in the object list to open it and click **Create Folder**.
#. In the **Folder Name** text box, enter a name for the folder.

   -  You can create single-level or multi-level folders.
   -  The name cannot contain the following special characters: ``\:*?"<>|``
   -  The name cannot start or end with a period (.) or slash (/).
   -  The folder's absolute path cannot exceed 1,023 characters.
   -  Any single slash (/) separates and creates multiple levels of folders at once.
   -  The name cannot contain two or more consecutive slashes (/).

#. Click **OK**.

Follow-up Procedure
-------------------

You can click **Copy Path** on the right to copy the path of the folder and share it with others. Then they can open the bucket where the folder is stored and enter the path in the search box above the object list to find the folder.

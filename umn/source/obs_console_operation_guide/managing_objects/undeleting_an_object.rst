:original_name: en-us_topic_0066176932.html

.. _en-us_topic_0066176932:

Undeleting an Object
====================

Scenarios
---------

If a bucket has :ref:`versioning <obs_03_0327>` enabled, you can recover a deleted object by undeleting it.

Background Information
----------------------

**Object Deletion with Versioning Enabled**

When versioning is enabled for a bucket, OBS works slightly different when deleting different objects.

-  Deleting a file or folder: The file or folder is not permanently deleted, but is retained in the **Deleted Objects** list and marked with the **Delete Marker**.

   -  To permanently delete the file or folder, delete it again from the **Deleted Objects** list. For details, see :ref:`Deleting an Object or Folder <en-us_topic_0045853756>`.
   -  To recover the deleted file, undelete it from the **Deleted Objects** list. For details, see :ref:`Procedure <en-us_topic_0066176932__section50464659154530>`.

-  Deleting an object version: The version will be permanently deleted and cannot be recovered. If the deleted version is the latest one, the next latest version becomes the latest version.

**Object Recovery with Versioning Enabled**

When a bucket has the versioning function enabled, deleting a file from the **Objects** list does not permanently delete it. The deleted file will be retained with the **Delete Marker** in the **Deleted Objects** list. You can recover the deleted file using the **Undelete** operation.

Note the following points when you undelete objects:

#. Only files can be undeleted but not folders.

   After you undelete a deleted file, the file is recovered and will appear in the **Objects** list. Then you can perform basic operations on the file as you normally do on other objects. If the file was stored in a folder before the deletion, it will be recovered to its original path after you undelete it.

#. Deleted files in the **Deleted Objects** also keep multiple versions. When deleting different versions of files, note the following points:

   -  If you delete a version with the **Delete Marker**, it actually recovers this version instead of permanently deleting it. For details, see :ref:`Related Operations <en-us_topic_0066176932__section27691114163422>`.
   -  If you delete a version without the **Delete Marker**, that version is permanently deleted. This version will not be recovered, even if the object is recovered later.

#. A deleted object must have at least one version without the **Delete Marker** in the **Deleted Objects** list. Otherwise, the object cannot be undeleted.

Prerequisites
-------------

-  Versioning has been enabled for the bucket. For details, see :ref:`Configuring Versioning <obs_03_0327>`.
-  The file to be recovered is in the **Deleted Objects** list, and has at least one version without the **Delete Marker**.

.. _en-us_topic_0066176932__section50464659154530:

Procedure
---------

#. In the bucket list, click the bucket you want to operate. The **Overview** page is displayed.

#. In the navigation pane, choose **Objects**.

#. Click **Deleted Objects**.

#. In the row of the deleted object that you want to recover, click **Undelete** on the right.

   You can select multiple files and click **Undelete** above the object list to batch recover them.

.. _en-us_topic_0066176932__section27691114163422:

Related Operations
------------------

**Recover a file by deleting its version with the Delete Marker:**

#. In the bucket list, click the bucket you want to operate. The **Overview** page is displayed.
#. In the navigation pane, choose **Objects**.
#. Click **Deleted Objects**.
#. Click the deleted file that you want to recover. The file information is displayed.
#. On the **Versions** tab, view all versions of the file.

   -  If you delete a version with the **Delete Marker**, the file will be recovered and retained in the **Objects** list.
   -  If you delete a version without the **Delete Marker**, that version will be permanently deleted.

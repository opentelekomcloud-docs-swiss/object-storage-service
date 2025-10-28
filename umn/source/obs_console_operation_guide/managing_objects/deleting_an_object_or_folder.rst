:original_name: en-us_topic_0045853756.html

.. _en-us_topic_0045853756:

Deleting an Object or Folder
============================

Scenarios
---------

On OBS Console, you can manually delete unneeded files or folders to release space and reduce costs.

Alternatively, you can configure lifecycle rules to periodically, automatically delete some or all of the files and folders from a bucket. For details, see :ref:`Configuring a Lifecycle Rule <obs_03_0335>`.

In big data scenarios, parallel file systems usually have deep directory levels and each directory has a large number of files. In such case, deleting directories from parallel file systems may fail due to timeout. To address this problem, you are advised to configure :ref:`a lifecycle rule <obs_03_0335>` for directories so that they can be deleted in background based on the preset lifecycle rule.

Background Information
----------------------

**Object Deletion with Versioning Enabled**

When versioning is enabled for a bucket, OBS works slightly different when deleting different objects.

-  Deleting a file or folder: The file or folder is not permanently deleted, but is retained in the **Deleted Objects** list and marked with the **Delete Marker**. In **Deleted Objects**, click the object name. On the **Versions** tab, you can see that the latest object version has the delete marker.

   -  To permanently delete the file or folder, delete it again from the **Deleted Objects** list. For details, see :ref:`Procedure <en-us_topic_0045853756__section56466209>`.
   -  To recover the deleted file, undelete it from the **Deleted Objects** list. For details, see :ref:`Undeleting an Object <en-us_topic_0066176932>`.

-  Deleting an object version: The version will be permanently deleted and cannot be recovered. If the deleted version is the latest one, the next latest version becomes the latest version.

.. _en-us_topic_0045853756__section56466209:

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

#. Select the file or folder you want to delete and choose **More** > **Delete** on the right.

   You can select multiple files or folders and click **Delete** above the object list to batch delete them.

#. Click **OK** to confirm the deletion.

   .. caution::

      If you delete an object from a bucket with versioning enabled, the object is not permanently deleted but retained in the **Deleted Objects** list. If you need to permanently delete the object to save space, complete the following steps:

#. If versioning is enabled for the bucket, delete the files or folders again from the **Deleted Objects** list to permanently delete them.

   .. note::

      In a bucket with WORM enabled, objects cannot be permanently deleted from the **Deleted Objects** list. You can permanently delete an object on its details page. For details, see :ref:`Related Operations <obs_03_0327__section29772226>` or :ref:`Configuring WORM Retention <obs_03_0718>`.

      Likewise, folders cannot be permanently deleted from the **Deleted Objects** list either. To permanently delete a folder, you can only :ref:`configure a lifecycle rule <obs_03_0335>`.

   a. Click **Deleted Objects**.

   b. In the **Operation** column of the file or folder to be deleted, click **Permanently Delete**.

      You can also select multiple files or folders and click **Permanently Delete** above the object list to batch delete them.

.. _en-us_topic_0045853756__section089519314196:

Related Operations
------------------

When versioning is enabled, files in the **Deleted Objects** list also have multiple versions. Note the following points when deleting different versions of files:

-  Deleting a version with the **Delete Marker** actually recovers this version instead of permanently deleting it. For details, see :ref:`Undeleting an Object <en-us_topic_0066176932>`.
-  Deleting a version without the **Delete Marker** permanently deletes this version. This version will not be recovered even if the object is recovered later.

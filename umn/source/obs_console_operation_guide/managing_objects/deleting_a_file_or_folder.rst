:original_name: en-us_topic_0045853756.html

.. _en-us_topic_0045853756:

Deleting a File or Folder
=========================

Scenarios
---------

On OBS Console, you can delete unneeded files or folders to release space and reduce costs.

This topic describes how to manually delete files or folders on OBS Console.

OBS also provides the lifecycle management function to meet your requirements for periodically and automatically deleting files from a bucket or clearing all files and folders in a bucket. For details, see :ref:`Configuring a Lifecycle Rule <obs_03_0335>`.

Background Information
----------------------

**Object deletion mechanism when versioning is enabled**

When versioning is enabled, OBS uses different deletion methods for different objects.

-  Deleting a file or folder does not delete it permanently. The deleted file or folder will be retained in the **Deleted Objects** list and marked with the **Delete Marker**. In **Deleted Objects**, click the object name. On the **Versions** tab, you can see that the latest object version has the delete marker.

   -  If you want to delete the file or folder permanently, you need to delete it from the **Deleted Objects** list. For details, see :ref:`Procedure <en-us_topic_0045853756__section56466209>` in this section.
   -  To recover a deleted file, you can cancel the deletion by the **Undelete** operation. For details, see :ref:`Undeleting a File <en-us_topic_0066176932>`.

-  Deleting a version of an object will permanently delete that version. If the deleted version is the latest one, the next latest version becomes the latest version.

.. _en-us_topic_0045853756__section56466209:

Procedure
---------

#. In the bucket list, click the bucket to be operated. The **Overview** page of the bucket is displayed.

#. In the navigation pane, click **Objects**.

#. Select the file or folder you want to delete, and choose **More** > **Delete** on the right.

   You can select multiple files or folders and click **Delete** above the object list to batch delete them.

#. Click **Yes** to confirm the deletion.

#. If versioning is enabled for the bucket, you need to delete files or folders from the **Deleted Objects** list in order to permanently delete them.

   a. Click **Deleted Objects**.

   b. In the **Operation** column of the file or folder to be deleted, click **Delete**.

      You can select multiple files or folders and click **Delete** above the object list to batch delete them.

.. _en-us_topic_0045853756__section089519314196:

Follow-up Procedure
-------------------

When versioning is enabled, files in the **Deleted Objects** list also have multiple versions. Note the following points when deleting different versions of files:

-  If you delete a version with the **Delete Marker**, it actually recovers that specific version instead of permanently deleting it. For details, see :ref:`Undeleting a File <en-us_topic_0066176932>`.
-  If you delete a version without the **Delete Marker**, that specific version is deleted permanently. Even if the object is recovered later, this version will not be recovered.

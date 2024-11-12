:original_name: obs_03_0309.html

.. _obs_03_0309:

Deleting an Object
==================

You can delete unnecessary files one by one or in a batch on OBS Console to save space and money.

.. note::

   When WORM has been enabled for a bucket, versioning is also enabled for the bucket by default. If an object version has any WORM retention policy configured, this object version cannot be permanently deleted during the retention period. On the **Versions** tab of the object details page, you can choose **More** > **Extend Retention Period** in the **Operation** column in the row of the object version to check whether this version is within the retention period. If no WORM retention policy is configured for an object version, you can delete it on the **Versions** tab of the object details page.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

#. Select the file you want to delete, and choose **More** > **Delete** on the right.

   You can select multiple files and click **Delete** above the file list to batch delete them.

#. Click **Yes** to confirm the deletion.

Important Notes
---------------

In big data scenarios, parallel file systems usually have deep directory levels and each directory has a large number of files. In such case, deleting directories from parallel file systems may fail due to timeout. To address this problem, you are advised to configure :ref:`a lifecycle rule <obs_03_0335>` for directories so that they can be deleted in background based on the preset lifecycle rule.

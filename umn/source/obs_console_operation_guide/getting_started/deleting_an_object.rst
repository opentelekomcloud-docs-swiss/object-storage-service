:original_name: obs_03_0309.html

.. _obs_03_0309:

Deleting an Object
==================

You can delete unnecessary files one by one or in a batch on OBS Console to save space and money.

.. note::

   When you enable WORM for a bucket, versioning is automatically enabled as well. If a WORM retention policy is configured, object versions cannot be permanently deleted during the retention period. On the object list page, you can enable **Historical Versions** and choose **More** > **Extend Retention Period** in the **Operation** column of a specific object version to check whether this version is within the retention period. If no WORM retention policy is configured, you can delete object versions on the object list page with **Historical Versions** enabled.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

#. Select the file you want to delete, and choose **More** > **Delete** on the right.

   You can select multiple files and click **Delete** above the file list to batch delete them.

#. Click **OK** to confirm the deletion.

Important Notes
---------------

In big data scenarios, parallel file systems usually have deep directory levels and each directory has a large number of files. In such case, deleting directories from parallel file systems may fail due to timeout. To address this problem, you are advised to configure :ref:`a lifecycle rule <obs_03_0335>` for directories so that they can be deleted in background based on the preset lifecycle rule.

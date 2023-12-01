:original_name: obs_03_0309.html

.. _obs_03_0309:

Deleting an Object
==================

You can delete unnecessary files one by one or in a batch on OBS Console to save space and money.

Procedure
---------

#. In the bucket list, click the bucket you want to operate. The **Overview** page is displayed.

#. In the navigation pane, choose **Objects**.

#. Select the file you want to delete, and choose **More** > **Delete** on the right.

   You can select multiple files and click **Delete** above the file list to batch delete them.

#. Click **Yes** to confirm the deletion.

Important Notes
---------------

In big data scenarios, parallel file systems usually have deep directory levels and each directory has a large number of files. In such case, deleting directories from parallel file systems may fail due to timeout. To address this problem, you are advised to configure :ref:`a lifecycle rule <obs_03_0335>` for directories so that they can be deleted in background based on the preset lifecycle rule.

:original_name: obs_03_1068.html

.. _obs_03_1068:

Restoring a File or Folder
==========================

Restore Cold objects before downloading them.

Context
-------

Cold storage is secure, durable, and inexpensive for storing data that is rarely accessed (once a year on average). It is suitable for data archiving and long-term backup. This storage class allows you to safely store your data at low cost. However, it may take hours to restore data stored in this class.

If a Cold object is being restored, you cannot suspend or delete the restore task.

Objects in the **Restoring** state cannot be restored again.

Procedure
---------

#. Log in to OBS Browser+.

#. Go to the object list in the target bucket.

#. Select the file or folder you want to restore and choose **More** > **Restore**.

   To restore an object, you must configure the validity period and restore speed. :ref:`Table 1 <obs_03_1068__table4222151134720>` describes relevant parameters.

   .. _obs_03_1068__table4222151134720:

   .. table:: **Table 1** Restoring an object

      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                |
      +===================================+============================================================================================================================================================================================================================================================+
      | Object Name                       | Name of the object or path to be restored.                                                                                                                                                                                                                 |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Validity Period                   | Time duration when an object remains in the **Restored** state after it has been restored. The validity period starts when the object is restored. You can set the validity period to an integer ranging from 1 to 30 (days). The default value is **30**. |
      |                                   |                                                                                                                                                                                                                                                            |
      |                                   | For example, you set **Validity Period** to **20** when restoring an object. 20 days after the object is restored, its status will change from **Restored** to **Unrestored**.                                                                             |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Speed                             | How fast an object will be restored.                                                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                                            |
      |                                   | -  **Expedited**: All Cold data can be restored within 1 to 5 minutes.                                                                                                                                                                                     |
      |                                   | -  **Standard**: All Cold data can be restored within 3 to 5 hours.                                                                                                                                                                                        |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK** to confirm the restored file or folder.

   To view the restoration status of the file or folder, click |image1| next to the object and choose **Object Properties** to view the restoration status. You can download the file only after it has been restored.

Follow-Up Procedure
-------------------

Within the validity period of a restored object, you can restore the object again. Each time the object is restored, its validity period will restart. This extends the validity period.

.. note::

   1. If a restored object is restored again, its expiration time should be later than the time set for the previous restoration. For example, if an object is scheduled to expire at **4/12/2021 08:00:00 GMT+08:00** after it is restored for the first time, it should expire later than **4/12/2021 08:00:00 GMT+08:00** after the second restore.

   2. You are advised not to restore a large number of files in one batch. When more than 10,000 objects are being restored, OBS Browser+ will take a long time to query the restoration progress of such objects. If you indeed need to restore such a large number of files in one batch, you are advised to use SDKs or APIs to query the restoration progress. You can also download files after the maximum restoration time, which is estimated based on the restoration rate you selected.

.. |image1| image:: /_static/images/en-us_image_0000002713118379.png

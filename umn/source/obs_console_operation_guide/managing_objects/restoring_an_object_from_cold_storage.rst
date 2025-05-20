:original_name: obs_03_0320.html

.. _obs_03_0320:

Restoring an Object from Cold Storage
=====================================

You must restore a Cold object before you can download it, access it with a URL, or configure its ACL or metadata.

Constraints
-----------

-  If a Cold object is being restored, its restore task cannot be suspended or deleted.
-  An object being restored cannot be restored again.
-  After an object is restored, an object copy in the Standard storage class will be generated. This way, there is a Cold object and also its Standard copy in the bucket. The copy will be automatically deleted once the restoration expires.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

#. Select the file you want to restore, and click **Restore** on the right.

   You can select multiple files and choose **More** > **Restore** above the file list to batch restore them.

   .. note::

      Objects that are being restored cannot be added for batch restore.

#. Configure the validity period and speed of the restore. The following table describes the parameters.

   .. table:: **Table 1** Parameters for restoring objects

      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                    |
      +===================================+================================================================================================================================================================================================+
      | Validity Period                   | How long the object will remain in the **Restored** state. It starts once the object is restored. The value is an integer ranging from 1 to 30 (days). The default value is **30**.            |
      |                                   |                                                                                                                                                                                                |
      |                                   | For example, if you set **Validity Period** to **20** when restoring an object, 20 days after the object is successfully restored, its status will change from **Restored** to **Unrestored**. |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Speed                             | How fast an object will be restored.                                                                                                                                                           |
      |                                   |                                                                                                                                                                                                |
      |                                   | -  **Expedited**: Cold objects can be restored within 1 to 5 minutes.                                                                                                                          |
      |                                   | -  **Standard**: Cold objects can be restored within 3 to 5 hours.                                                                                                                             |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

   The **Restoration Status** field in the object details page displays the restore status of the object.

   You can click |image1| to manually refresh the restore status.

   .. note::

      The system checks the file restore status at UTC 00:00 every day. The system starts counting down the expiration time from the time when the latest check is complete.

Related Operations
------------------

Within the validity period of a restored object, you can restore the object again. The validity period is then extended because it will start again when the latest restore is complete.

.. note::

   If a restored object is restored again, its expiration time should be later than the time set for the previous restore. Assume that an object is restored on January 1 and will expire 30 days later (on January 30). If the object is restored again on January 10 and is made to be expired earlier than January 30 (less than 20 days later), this restore action is considered invalid.

.. |image1| image:: /_static/images/en-us_image_0148639825.png

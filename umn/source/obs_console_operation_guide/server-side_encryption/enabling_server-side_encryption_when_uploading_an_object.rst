:original_name: obs_03_0322.html

.. _obs_03_0322:

Enabling Server-Side Encryption When Uploading an Object
========================================================

OBS allows you to encrypt objects with server-side encryption so that the objects can be securely stored in OBS.

When you upload an object to a bucket with server-side encryption disabled, you can separately configure server-side encryption for the object. If the bucket has server-side encryption enabled, the object you upload inherits encryption from the bucket by default. You can also configure new encryption for the object.

Constraints
-----------

-  The object encryption status cannot be changed.
-  A key in use cannot be deleted. Otherwise, the object encrypted with this key cannot be downloaded.

Prerequisites
-------------

In the region where OBS is deployed, the **KMS Administrator** permission has been added to the user group. For details about how to add permissions, see the *IAM User Guide*.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

#. Click **Upload Object**. The **Upload Object** dialog box is displayed.

#. Add the files to be uploaded.

#. Choose **SSE-KMS**. You can select the default key in the current region to encrypt the objects you upload to the bucket. If you do not have a default key, OBS automatically creates one the first time you upload an object. You can also choose **Custom** to use a custom key for encryption. If there is no custom key available, click **Create KMS Key** to create one on the DEW console. Then, go back here and choose the created key from the drop-down list.

   .. note::

      If the bucket has server-side encryption configured, the object you upload will inherit encryption from the bucket by default.

#. Click **Upload**.

   After the object is uploaded, you can view its encryption status on its details page.

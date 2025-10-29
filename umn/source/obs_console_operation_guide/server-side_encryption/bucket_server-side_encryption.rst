:original_name: obs_03_0088.html

.. _obs_03_0088:

Bucket Server-Side Encryption
=============================

You can configure server-side encryption for an OBS bucket. Once configured, any objects you upload to the bucket will be encrypted with the specified KMS key by default.

You can enable encryption (by choosing SSE-KMS) when creating a bucket (see :ref:`Creating a Bucket <en-us_topic_0045853662>`). You can also enable or disable encryption for an existing bucket.

OBS only encrypts the objects uploaded after server-side encryption is enabled for the bucket, and does not encrypt those uploaded before. After server-side encryption is disabled, encryption status of existing objects in the bucket remains unchanged, and you can still encrypt objects when you upload them.

Enabling Server-Side Encryption for a Bucket
--------------------------------------------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

#. In the navigation pane, choose **Overview**.

#. In the **Basic Configurations** area, click **Server-Side Encryption**. The **Server-Side Encryption** dialog box is displayed.

#. Select **SSE-KMS**.

   You can select **Default** to use the default key in the current region to encrypt the objects you upload. If you do not have a default key, OBS creates one the first time you upload an object. You can also choose **Custom** to use a custom key for encryption. If there is no custom key available, click **Create KMS Key** to create one on the DEW console. Then, go back here and choose the created key from the drop-down list.

#. Click **OK**.

Disabling Server-Side Encryption for a Bucket
---------------------------------------------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.
#. In the navigation pane, choose **Overview**.
#. In the **Basic Configurations** area, click **Server-Side Encryption**. The **Server-Side Encryption** dialog box is displayed.
#. Select **Disable**.
#. Click **OK**.

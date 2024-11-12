:original_name: en-us_topic_0045853663.html

.. _en-us_topic_0045853663:

Uploading an Object
===================

This section describes how to upload local files to OBS over the Internet. These files can be texts, images, videos, or any other type of files.

Constraints
-----------

-  You can upload a file of up to 50 MB using OBS Console.
-  You cannot batch upload files in OBS Console. To upload multiple files at a time, use OBS Browser+, or use APIs.
-  If versioning is disabled for your bucket and you upload a new file with the same name as the one you previously uploaded to your bucket, the new file automatically overwrites the previous one and does not retain its ACL information. If you upload a new folder using the same name that was used with a previous folder in the bucket, the two folders will be merged, and files in the new folder will overwrite those with the same name in the previous folder.
-  After versioning is enabled for your bucket, if the new file you upload has the same name as the one you previously uploaded to the bucket, a new file version will be added in the bucket. For details, see :ref:`Versioning Overview <en-us_topic_0045853504>`.

Prerequisites
-------------

-  At least one bucket has been created.
-  If you want to classify files, you can create folders and upload files to different folders. For details, see :ref:`Creating a Folder <obs_03_0316>`.

Procedure
---------

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.

#. Go to the folder where you want to upload files and click **Upload Object**. The **Upload Object** dialog box is displayed.

   .. note::

      If the files that you want to upload to OBS are stored in Microsoft OneDrive, it is recommended that the names of these files contain a maximum of 32 characters to ensure compatibility.


   .. figure:: /_static/images/en-us_image_0000001180660152.png
      :alt: **Figure 1** Uploading objects

      **Figure 1** Uploading objects

#. Select a storage class. If you do not specify a storage class, the objects you upload inherit the default storage class of the bucket.

   .. note::

      An object can have a different storage class from its bucket. You can specify a storage class for an object when uploading it, or you can change the object storage class after the object is uploaded.

#. In the **Upload Object** area, drag and drop the files or folders you want to upload.

   You can also click **add files** to select files.

#. **Server-Side Encryption**: Choose **SSE-KMS** or **Disable**. For details, see :ref:`Enabling Server-Side Encryption When Uploading an Object <obs_03_0322>`.

   .. note::

      If the bucket has server-side encryption configured, the object you upload will inherit encryption from the bucket by default.

#. (Optional) To configure metadata or WORM retention policies, click **Next: (Optional) Configure Advanced Settings**.

   .. note::

      WORM retention policies can be configured in the advanced settings only when WORM is enabled for the bucket.

   Configuring metadata: Add metadata ContentDisposition, ContentLanguage, WebsiteRedirectLocation, ContentEncoding, or ContentType as needed. For more information, see :ref:`Object Metadata <en-us_topic_0049066876>`. Metadata is a set of name-value pairs. The metadata value cannot be left blank. You can add two or more metadata entries by clicking **Add**.

   Configuring WORM retention: Choose **Inherit from bucket**, or choose **Configure** and then specify a retention period, to automatically protect new objects uploaded to the bucket from being deleted.


   .. figure:: /_static/images/en-us_image_0000001925837700.png
      :alt: **Figure 2** Configuring metadata or WORM retention

      **Figure 2** Configuring metadata or WORM retention

#. Click **Upload**.

Related Operations
------------------

When uploading an object, you can specify a storage class for it. After the object is uploaded, you can also change its storage class by doing as follows:

#. In the bucket list, click the bucket you want to operate to go to the **Objects** page.
#. Select the target object and choose **More** > **Change Storage Class** on the right.
#. Select the desired storage class and click **OK**.

.. note::

   -  You can manually change objects between storage classes.

      -  From Standard to Warm or Cold
      -  From Warm to Standard or Cold
      -  From Cold to Standard or Warm. Before changing Cold objects, you must restore them first.

   -  After an object is changed to Cold, its restore status changes to **Unrestored**.
   -  You can also configure a lifecycle rule to change the storage class of an object. For details, see :ref:`Configuring a Lifecycle Rule <obs_03_0335>`.

Follow-up Procedure
-------------------

You can click **Copy Path** on the right of an object to copy its path.

You can share the path with others. Then they can open the bucket where the object is stored and enter the path in the search box above the object list to find the object.

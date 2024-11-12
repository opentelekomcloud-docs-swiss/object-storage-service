:original_name: en-us_topic_0066088967.html

.. _en-us_topic_0066088967:

Bucket ACLs and Object ACLs
===========================

Access control lists (ACLs) enable you to manage access to buckets and objects, and define grantees and their granted access permissions. Each bucket and object has its own ACL that defines which accounts or groups are granted access and the type of access. When a request is received against a resource, OBS checks the ACL of the resource to verify whether the requester has necessary access permissions.

When you create a bucket or an object, OBS creates a default ACL that grants the resource owner full control (FULL_CONTROL) over the bucket or object.

An ACL supports up to 100 grants.

Who Is a Principal?
-------------------

A principal can be an account or one of the predefined OBS groups. For details, see :ref:`Table 1 <en-us_topic_0066088967__table177445813209>`.

.. _en-us_topic_0066088967__table177445813209:

.. table:: **Table 1** Users supported by OBS

   +-----------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Principal                                                                         | Description                                                                                                                                                                                                                                                                                                                                                                                                          |
   +===================================================================================+======================================================================================================================================================================================================================================================================================================================================================================================================================+
   | Specific User                                                                     | You can grant accounts access permissions to a bucket or an object using ACLs. Once a specific account is granted the access permissions, all IAM users who have OBS resource permissions under this account can have the same access permissions to operate the bucket or object.                                                                                                                                   |
   |                                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                      |
   |                                                                                   | If you need to grant different access permissions to different IAM users, configure bucket policies. For details, see :ref:`Granting an IAM User Permissions to Operate a Specific Bucket <obs_03_0080>`.                                                                                                                                                                                                            |
   +-----------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Owner                                                                             | The owner of a bucket is the account that created the bucket. The bucket owner has all bucket access permissions by default. The read and write permissions for the bucket ACL are permanently available to the bucket owner, and cannot be modified.                                                                                                                                                                |
   |                                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                      |
   |                                                                                   | The owner of an object is the account that uploads the object, who may not be the owner of the bucket to which the object belongs. The object owner has the read access to the object, as well as the read and write access to the object ACL, and such access permissions cannot be modified.                                                                                                                       |
   |                                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                      |
   |                                                                                   | .. important::                                                                                                                                                                                                                                                                                                                                                                                                       |
   |                                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                      |
   |                                                                                   |    NOTICE:                                                                                                                                                                                                                                                                                                                                                                                                           |
   |                                                                                   |    Do not modify the bucket owner's read and write access permissions for the bucket.                                                                                                                                                                                                                                                                                                                                |
   +-----------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Anonymous User                                                                    | If anonymous users are granted access to a bucket or an object, anyone can access the object or bucket without identity authentication.                                                                                                                                                                                                                                                                              |
   +-----------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Log Delivery User                                                                 | A log delivery user only delivers access logs of buckets and objects to the specified target bucket. OBS does not create or upload any file to a bucket automatically. Therefore, if you want to record bucket access logs, you need to grant the permission to the log delivery user who will deliver the access logs to your specified target bucket. The user only delivers logs within the service scope of OBS. |
   |                                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                      |
   | .. note::                                                                         | .. important::                                                                                                                                                                                                                                                                                                                                                                                                       |
   |                                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                      |
   |    Only the bucket ACL supports authorizing permissions to the log delivery user. |    NOTICE:                                                                                                                                                                                                                                                                                                                                                                                                           |
   |                                                                                   |    After logging is enabled, the log delivery user group will be automatically granted the permission to read the bucket ACL and write the bucket where logs are saved. If you manually disable such permissions, bucket logging will fail.                                                                                                                                                                          |
   +-----------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

What Permissions Can I Grant Using an ACL?
------------------------------------------

:ref:`Table 2 <en-us_topic_0066088967__table28226836>` lists the permissions you can grant using a bucket ACL.

.. _en-us_topic_0066088967__table28226836:

.. table:: **Table 2** Access permissions controlled by a bucket ACL

   +-----------------------+-----------------------+-------------------------------------------------------------------------+
   | Permission            | Option                | Description                                                             |
   +=======================+=======================+=========================================================================+
   | Access to Bucket      | READ                  | Used to obtain the list of objects in a bucket and the bucket metadata. |
   +-----------------------+-----------------------+-------------------------------------------------------------------------+
   |                       | WRITE                 | Used to upload, overwrite, and delete any object in a bucket.           |
   +-----------------------+-----------------------+-------------------------------------------------------------------------+
   | Access to ACL         | READ_ACP              | Used to obtain the ACL of a bucket.                                     |
   |                       |                       |                                                                         |
   |                       |                       | The bucket owner has this permission permanently by default.            |
   +-----------------------+-----------------------+-------------------------------------------------------------------------+
   |                       | WRITE_ACP             | Used to update the ACL of a bucket.                                     |
   |                       |                       |                                                                         |
   |                       |                       | The bucket owner has this permission permanently by default.            |
   +-----------------------+-----------------------+-------------------------------------------------------------------------+

:ref:`Table 3 <en-us_topic_0066088967__table63381242464>` lists the permissions you can grant using an object ACL.

.. _en-us_topic_0066088967__table63381242464:

.. table:: **Table 3** Access permissions controlled by an object ACL

   +-----------------------+-----------------------+--------------------------------------------------------------+
   | Permission            | Option                | Description                                                  |
   +=======================+=======================+==============================================================+
   | Access to Object      | READ                  | Used to obtain the content and metadata of an object.        |
   +-----------------------+-----------------------+--------------------------------------------------------------+
   | Access to ACL         | READ_ACP              | Used to obtain the ACL of an object.                         |
   |                       |                       |                                                              |
   |                       |                       | The object owner has this permission permanently by default. |
   +-----------------------+-----------------------+--------------------------------------------------------------+
   |                       | WRITE_ACP             | Used to update the ACL of an object.                         |
   |                       |                       |                                                              |
   |                       |                       | The object owner has this permission permanently by default. |
   +-----------------------+-----------------------+--------------------------------------------------------------+

.. note::

   Every time you change the bucket or object access permission setting in an ACL, it overwrites the existing setting instead of adding a new access permission to the bucket or object.

   Fragment management refers to the deletion of fragments. For the bucket owner and users who have the permission to initiate multipart tasks, deleting fragments is not restricted by bucket ACL settings. If a user has the permission to write, the user also has the permission to initiate multipart tasks.

You can also set an ACL through a header when invoking the API for creating a bucket or uploading an object. Six types of predefined permissions can be set. Even with the predefined permissions configured, the bucket or object owner still has the full control over the resource. :ref:`Table 4 <en-us_topic_0066088967__table40200743>` lists the predefined permissions.

.. _en-us_topic_0066088967__table40200743:

.. table:: **Table 4** Predefined access permissions in OBS

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Predefined Access Permission      | Description                                                                                                                                                                                                                                                                                                                                               |
   +===================================+===========================================================================================================================================================================================================================================================================================================================================================+
   | private                           | Indicates that the owner of a bucket or an object has the full control over the resource. Any other users cannot access the bucket or object. This is the default access control policy.                                                                                                                                                                  |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | public-read                       | If this permission is granted on a bucket, anyone can obtain the object list, multipart tasks, metadata, and object versions in the bucket.                                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                                                                                                                                           |
   |                                   | If it is granted on an object, anyone can obtain the content and metadata of the object.                                                                                                                                                                                                                                                                  |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | public-read-write                 | If this permission is granted on a bucket, anyone can obtain the object list, multipart tasks, metadata, and object versions in the bucket, and can upload or delete objects, initialize multipart upload tasks, upload parts, merge parts, copy parts, and cancel multipart upload tasks.                                                                |
   |                                   |                                                                                                                                                                                                                                                                                                                                                           |
   |                                   | If it is granted on an object, anyone can obtain the content and metadata of the object.                                                                                                                                                                                                                                                                  |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | public-read-delivered             | If this permission is granted on a bucket, anyone can obtain the object list, multipart tasks, metadata, and object versions, and obtain the object content and metadata in the bucket.                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                                                                                                                           |
   |                                   | It does not apply to objects.                                                                                                                                                                                                                                                                                                                             |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | public-read-write-delivered       | If this permission is granted on a bucket, anyone can obtain the object list, multipart tasks, metadata, and object versions in the bucket, and can upload or delete objects, initialize multipart upload tasks, upload parts, merge parts, copy parts, and cancel multipart upload tasks. You can also obtain object content and metadata in the bucket. |
   |                                   |                                                                                                                                                                                                                                                                                                                                                           |
   |                                   | It does not apply to objects.                                                                                                                                                                                                                                                                                                                             |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | bucket-owner-full-control         | If this permission is granted on a bucket, the bucket can be accessed only by its owner.                                                                                                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                                                                                                                                           |
   |                                   | If it is granted on an object, only the bucket or object owner has the full control over the object.                                                                                                                                                                                                                                                      |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Bucket ACL Application Scenarios
--------------------------------

ACLs control the read and write permissions for accounts and groups. ACL permission granularity is not as fine as bucket policies and IAM policies. Generally, it is recommended that you use IAM policies and bucket policies for access control.

You can configure the bucket ACL to:

-  Grant an account the read and write access to the bucket, so that data in the bucket can be shared or the bucket can be added as an external bucket.

Object ACL Application Scenarios
--------------------------------

ACLs control the read and write permissions for accounts and groups. ACL permission granularity is not as fine as bucket policies and IAM policies. Generally, it is recommended that you use IAM policies and bucket policies for access control.

It is recommended that you use object ACLs in the following scenarios:

-  Object-level access control is required. A bucket policy can control access permissions for an object or a set of objects. If you want to further specify an access permission for an object in the set of objects for which a bucket policy has been configured, then the object ACL is recommended for easier access control over single objects.
-  An object is accessed through a URL. Generally, if you want to grant anonymous users the permission to read an object through a URL, use the object ACL.

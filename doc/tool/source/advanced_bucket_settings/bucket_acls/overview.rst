:original_name: obs_03_1048.html

.. _obs_03_1048:

Overview
========

An ACL defines grantees and their granted permissions.

Bucket and object ACLs are associated with accounts. By default, an ACL is created when a bucket or object is created, authorizing the owner full control over the bucket or object.

For easy and practical authorization, OBS ACLs have the following features:

-  An ACL takes effect for both a tenant and users under this tenant.
-  If a bucket and its objects have the same owner, the bucket's ACL also applies to the objects by default.
-  An ACL is created during bucket or object creation by default. You can also configure one after the bucket or object is created.

ACLs control write and read permissions based on accounts, whose permission granularity is not as fine as :ref:`bucket policies <obs_03_1054>` or IAM permissions. Generally, it is recommended that you use IAM permissions and bucket policies for access control.

You can grant bucket access permissions to users or user groups listed in :ref:`Table 1 <obs_03_1048__table177445813209>` by configuring an ACL.

.. _obs_03_1048__table177445813209:

.. table:: **Table 1** Authorized users supported by OBS

   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Principal                         | Description                                                                                                                                                                                                                                                                                     |
   +===================================+=================================================================================================================================================================================================================================================================================================+
   | Specific users                    | ACLs can be used to grant accounts access permissions on buckets or objects. Once a specific account is granted the access permissions, all IAM users who have OBS resource permissions under this account can have the same access permissions to operate the bucket or object.                |
   |                                   |                                                                                                                                                                                                                                                                                                 |
   |                                   | If you need to grant different access permissions to IAM users, configure bucket policies.                                                                                                                                                                                                      |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Owner                             | The owner of a bucket is the account that created the bucket. By default, a bucket owner has full control over the bucket ACL. The read and write permissions for the bucket ACL are permanently available to the bucket owner, and cannot be modified.                                         |
   |                                   |                                                                                                                                                                                                                                                                                                 |
   |                                   | An object owner is the account that uploads the object, but may not be the owner of the bucket that stores the object. The object owner has the read permission on the object, as well as the read and write permissions on the object ACL by default, and such permissions cannot be modified. |
   |                                   |                                                                                                                                                                                                                                                                                                 |
   |                                   | .. important::                                                                                                                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                                                                                 |
   |                                   |    NOTICE:                                                                                                                                                                                                                                                                                      |
   |                                   |    Do not modify the bucket owner's read and write permissions for the bucket.                                                                                                                                                                                                                  |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Anonymous users                   | Visitors who have not registered.                                                                                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                                                                                 |
   |                                   | .. important::                                                                                                                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                                                                                 |
   |                                   |    NOTICE:                                                                                                                                                                                                                                                                                      |
   |                                   |    If anonymous users are granted the permissions to access a bucket and objects, anyone can access the bucket or objects without identity authentication.                                                                                                                                      |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

:ref:`Table 2 <obs_03_1048__table28226836>` lists the access permissions controlled by a bucket ACL.

.. _obs_03_1048__table28226836:

.. table:: **Table 2** Access permissions controlled by a bucket ACL

   +-----------------------+-----------------------+-------------------------------------------------------------------------------------+
   | Permission            | Option                | Description                                                                         |
   +=======================+=======================+=====================================================================================+
   | Access to bucket      | Read                  | Allows a grantee to obtain the list of objects in a bucket and the bucket metadata. |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------+
   |                       | Object read           | Allows a grantee to obtain the object content and metadata.                         |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------+
   |                       | Write                 | Allows a grantee to upload, overwrite, and delete any object in a bucket.           |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------+
   | Access to ACL         | Read                  | Allows a grantee to obtain the bucket ACL.                                          |
   |                       |                       |                                                                                     |
   |                       |                       | The bucket owner has this permission permanently by default.                        |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------+
   |                       | Write                 | Allows a grantee to update the bucket ACL.                                          |
   |                       |                       |                                                                                     |
   |                       |                       | The bucket owner has this permission permanently by default.                        |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------+

:ref:`Table 3 <obs_03_1048__table63381242464>` lists the access permissions controlled by an object ACL.

.. _obs_03_1048__table63381242464:

.. table:: **Table 3** Access permissions controlled by an object ACL

   +-----------------------+-----------------------+-------------------------------------------------------------------+
   | Permission            | Option                | Description                                                       |
   +=======================+=======================+===================================================================+
   | Access to object      | Read                  | Allows a grantee to obtain the content and metadata of an object. |
   +-----------------------+-----------------------+-------------------------------------------------------------------+
   | Access to ACL         | Read                  | Allows a grantee to obtain the object ACL.                        |
   |                       |                       |                                                                   |
   |                       |                       | The object owner has this permission permanently by default.      |
   +-----------------------+-----------------------+-------------------------------------------------------------------+
   |                       | Write                 | Allows a grantee to update the object ACL.                        |
   |                       |                       |                                                                   |
   |                       |                       | The object owner has this permission permanently by default.      |
   +-----------------------+-----------------------+-------------------------------------------------------------------+

:original_name: obs_03_1057.html

.. _obs_03_1057:

Overview
========

If you have ACL permissions on buckets of other users, you can add them through OBS Browser+ as external buckets. By doing so, you can access these external buckets locally using your account.

By default, after user A has added a bucket of user B and uploaded an object to the bucket, user B cannot download the object.

You can grant read and write permissions to a bucket through the bucket ACL or bucket policy. Permissions controlled by a bucket ACL are as follows:

.. table:: **Table 1** Permissions controlled by a bucket ACL

   +-----------------------+-----------------------+-----------------------------------------+
   | Bucket ACL Permission | Option                | Mapped Action in a Custom Bucket Policy |
   +=======================+=======================+=========================================+
   | Access to bucket      | Read                  | -  HeadBucket                           |
   |                       |                       | -  ListBucket                           |
   |                       |                       | -  ListBucketVersions                   |
   |                       |                       | -  ListBucketMultipartUploads           |
   +-----------------------+-----------------------+-----------------------------------------+
   |                       | Write                 | -  PutObject                            |
   |                       |                       | -  DeleteObject                         |
   |                       |                       | -  DeleteObjectVersion                  |
   +-----------------------+-----------------------+-----------------------------------------+
   | Access to ACL         | Read                  | GetBucketAcl                            |
   +-----------------------+-----------------------+-----------------------------------------+
   |                       | Write                 | PutBucketAcl                            |
   +-----------------------+-----------------------+-----------------------------------------+

Permissions controlled by a standard bucket policy are as follows:

.. table:: **Table 2** Permissions controlled by a standard bucket policy

   +-----------------------+------------------------------+------------------------------+
   | Parameter             | Public Read                  | Public Read and Write        |
   +=======================+==============================+==============================+
   | Effect                | Allow                        | Allow                        |
   +-----------------------+------------------------------+------------------------------+
   | Principal             | \* (Any user)                | \* (Any user)                |
   +-----------------------+------------------------------+------------------------------+
   | Resources             | \* (All objects in a bucket) | \* (All objects in a bucket) |
   +-----------------------+------------------------------+------------------------------+
   | Actions               | -  GetObject                 | -  GetObject                 |
   |                       | -  GetObjectVersion          | -  GetObjectVersion          |
   |                       | -  HeadBucket                | -  PutObject                 |
   |                       | -  ListBucket                | -  DeleteObject              |
   |                       |                              | -  DeleteObjectVersion       |
   |                       |                              | -  HeadBucket                |
   |                       |                              | -  ListBucket                |
   +-----------------------+------------------------------+------------------------------+
   | Conditions            | N/A                          | N/A                          |
   +-----------------------+------------------------------+------------------------------+

If a custom bucket policy is used to authorize such permissions, the HeadBucket, ListBucket, GetObject, and GetObjectVersion actions must be allowed. More actions can be allowed according to your actual needs.

The following are some restrictions when you (the user who adds the bucket) operate the external bucket:

-  You cannot restore Archive objects that are not yours in the external bucket. You can view the object restore status only when the owner of those Archive objects grants you the read permission for the objects.
-  You can perform only authorized actions on existing objects in the external bucket. To perform any additional operations on an object, you must obtain the corresponding permissions from the object owner.
-  If you upload an object to the external bucket, the object ACL permissions will be automatically granted to the bucket owner, including the read permission for the object and the read and write permissions for the object ACL.
-  The encrypted objects you uploaded to the external bucket cannot be accessed by the bucket owner, because the bucket owner lacks the key.
-  To download an object from the external bucket, you must have read permission for that object. Encrypted objects in the external bucket cannot be downloaded.

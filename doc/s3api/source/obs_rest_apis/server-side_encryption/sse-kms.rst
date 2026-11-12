:original_name: en-us_topic_0125560445.html

.. _en-us_topic_0125560445:

SSE-KMS
=======

In SSE-KMS mode, OBS uses the keys provided by KMS for server-side encryption. When an object encrypted using SSE-KMS is added to a bucket in a region for the first time, OBS creates a default customer master key (CMK), which is used to encrypt and decrypt the keys provided by KMS. Only users with the tenant_admin role can use SSE-KMS interfaces. The SSE-KMS mode does not support the keys created by customers. The bucket ACL and policy do not allow cross-tenant authorized access to objects encrypted using SSE-KMS. OBS does not support KMS with multiple projects.

:ref:`Table 1 <en-us_topic_0125560445__table3087586113454>` lists two headers that are added to support SSE-KMS in SSE-KMS mode.

.. _en-us_topic_0125560445__table3087586113454:

.. table:: **Table 1** Headers needed in SSE-KMS mode

   +---------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Header                                      | Description                                                                                                                                                                    |
   +=============================================+================================================================================================================================================================================+
   | x-amz-server-side-encryption                | Indicates that SSE-KMS is used. Objects are encrypted using SSE-KMS.                                                                                                           |
   |                                             |                                                                                                                                                                                |
   |                                             | Example:                                                                                                                                                                       |
   |                                             |                                                                                                                                                                                |
   |                                             | x-amz-server-side-encryption:aws:kms                                                                                                                                           |
   +---------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | x-amz-server-side-encryption-aws-kms-key-id | Indicates the master key ID of an encrypted object. This header is used in SSE-KMS mode. If the customer does not provide the master key, the default master key will be used. |
   |                                             |                                                                                                                                                                                |
   |                                             | Example:                                                                                                                                                                       |
   |                                             |                                                                                                                                                                                |
   |                                             | x-amz-server-side-encryption-aws-kms-key-id:arn:aws:kms:sichuan:domainiddomainiddomainiddoma0001:key/4f1cd4de-ab64-4807-920a-47fc42e7f0d0                                      |
   |                                             |                                                                                                                                                                                |
   |                                             | Note:                                                                                                                                                                          |
   |                                             |                                                                                                                                                                                |
   |                                             | sichuan: indicates the region name. Set the value based on site requirements.                                                                                                  |
   |                                             |                                                                                                                                                                                |
   |                                             | domainiddomainiddomainiddoma0001: indicates the tenant ID. Set the value based on site requirements.                                                                           |
   |                                             |                                                                                                                                                                                |
   |                                             | key/4f1cd4de-ab64-4807-920a-47fc42e7f0d0: indicates the key ID. Set the value based on site requirements.                                                                      |
   +---------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 2** Interfaces to which the newly added headers apply

   +---------------------------------------------------------------------+
   | Interface                                                           |
   +=====================================================================+
   | PUT Object                                                          |
   +---------------------------------------------------------------------+
   | POST Object                                                         |
   +---------------------------------------------------------------------+
   | PUT Object - Copy (the newly added headers apply to target objects) |
   +---------------------------------------------------------------------+
   | Initiate Multipart Upload                                           |
   +---------------------------------------------------------------------+

OBS supports bucket policies. If you want to restrict server-side encryption for all objects stored in a bucket, you can use bucket policies. For example, if an object upload request does not contain **x-amz-server-side-encryption:"aws:kms"**, the header for requesting server-side encryption (SSE-KMS), the following bucket policy rejects the upload request:

.. code-block::

   {
   "Version":"2008-10-17",
   "Id":"PutObjPolicy",
   "Statement": [
           {
               "Sid": "DenyUnEncryptedObjectUploads",
               "Effect": "Deny",
               "Principal": "*",
               "Action": "s3:PutObject",
               "Resource": "arn:aws:s3:::YourBucket/*",
               "Condition": {
                   "StringNotEquals": {
                       "s3:x-amz-server-side-encryption": "aws:kms"
                   }
               }
           }
       ]
   }

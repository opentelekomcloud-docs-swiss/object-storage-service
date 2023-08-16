:original_name: obs_03_0325.html

.. _obs_03_0325:

Relationship Between a Bucket ACL and a Bucket Policy
=====================================================

Mapping Relationship Between Bucket ACLs and Bucket Policies
------------------------------------------------------------

Bucket ACLs are used to control basic read and write access permissions for buckets. Custom settings of bucket policies support more actions that can be performed on buckets. Bucket policies, supplements to bucket ACLs, can replace the bucket ACL to manage the access permissions of a bucket. :ref:`Table 1 <obs_03_0325__table183716545593>` shows the mapping between bucket ACL access permissions and bucket policy actions.

.. _obs_03_0325__table183716545593:

.. table:: **Table 1** Mapping relationship between bucket ACLs and bucket policies

   +-----------------------+-----------------------+-----------------------------------------+
   | ACL Permission        | Option                | Mapped Action in a Custom Bucket Policy |
   +=======================+=======================+=========================================+
   | Access to bucket      | Read                  | -  ListBucket                           |
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

Mapping Relationship Between Object ACLs and Bucket Policies
------------------------------------------------------------

Object ACLs are used to control basic read and write access permissions for objects. The custom settings of bucket policies support more actions that can be performed on objects. :ref:`Table 2 <obs_03_0325__table4160714016>` describes the mapping relationship between object ACL access permissions and bucket policy actions.

.. _obs_03_0325__table4160714016:

.. table:: **Table 2** Mapping relationship between object ACLs and bucket policies

   +-----------------------+-----------------------+-----------------------------------------+
   | Object ACL            | Option                | Mapped Action in a Custom Bucket Policy |
   +=======================+=======================+=========================================+
   | Access to Object      | Read                  | -  GetObject                            |
   |                       |                       | -  GetObjectVersion                     |
   +-----------------------+-----------------------+-----------------------------------------+
   | Access to ACL         | Read                  | -  GetObjectAcl                         |
   |                       |                       | -  GetObjectVersionAcl                  |
   +-----------------------+-----------------------+-----------------------------------------+
   |                       | Write                 | -  PutObjectAcl                         |
   |                       |                       | -  PutObjectVersionAcl                  |
   +-----------------------+-----------------------+-----------------------------------------+

Does Bucket Policy Change Effect on the ACL Setting?
----------------------------------------------------

When objects are uploaded to a bucket, object ACLs are set for those objects. When the bucket policy is modified, ACLs of the objects do not change. However, ACLs of newly uploaded objects will be the default setting, and will not inherit the object ACL rule set by existing objects.

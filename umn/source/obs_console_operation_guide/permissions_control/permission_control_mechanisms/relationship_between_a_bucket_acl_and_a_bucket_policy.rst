:original_name: obs_03_0325.html

.. _obs_03_0325:

Relationship Between a Bucket ACL and a Bucket Policy
=====================================================

Mapping Between Bucket ACLs and Bucket Policies
-----------------------------------------------

Bucket ACLs are used to control basic read and write access to buckets. Custom settings of bucket policies support more actions that can be performed on buckets. Bucket policies supplement bucket ACLs. In most cases (granting permissions to log delivery user groups excluded), you can use bucket policies to manage access to buckets. :ref:`Table 1 <obs_03_0325__table8311113173517>` shows the mapping between bucket ACL access permissions and bucket policy actions.

.. _obs_03_0325__table8311113173517:

.. table:: **Table 1** Mapping between bucket ACL access permissions and bucket policy actions

   +-----------------------+-----------------------+-----------------------------------------+
   | ACL Permission        | Option                | Mapped Action in a Custom Bucket Policy |
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
   | Access to object      | Object read           | -  GetObject                            |
   +-----------------------+-----------------------+-----------------------------------------+
   | Access to ACL         | Read                  | -  GetBucketAcl                         |
   +-----------------------+-----------------------+-----------------------------------------+
   |                       | Write                 | -  PutBucketAcl                         |
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

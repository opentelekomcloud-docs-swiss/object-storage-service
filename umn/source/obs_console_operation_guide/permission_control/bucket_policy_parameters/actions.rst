:original_name: obs_03_0051.html

.. _obs_03_0051:

Actions
=======

Actions are related to resources. When the resource is the current bucket, actions configured in the bucket policy must be bucket related actions. When objects are specified as resources, actions configured in the bucket policy must be object related actions.

Actions can be specified in either of the following ways:

-  **Include**: Specifies the actions on which the bucket policy takes effect.
-  **Exclude**: Specifies that on all except the specified actions the bucket policy takes effect.

Actions Related to Buckets
--------------------------

.. table:: **Table 1** Actions related to buckets

   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   | Type    | Value                      | Description                                                                                          |
   +=========+============================+======================================================================================================+
   | General | \*                         | The value supports a wildcard character (``*``) that indicates all operations can be performed.      |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | Get\*                      | The value supports a wildcard character (``*``) that indicates all GET operations can be performed.  |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | Put\*                      | The value supports a wildcard character (``*``) that indicates all PUT operations can be performed.  |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | List\*                     | The value supports a wildcard character (``*``) that indicates all LIST operations can be performed. |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   | Bucket  | DeleteBucket               | Deletes the bucket.                                                                                  |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | ListBucket                 | Lists objects in the bucket, and gets the bucket metadata.                                           |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | ListBucketVersions         | Lists object versions in the bucket.                                                                 |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | ListBucketMultipartUploads | Lists multipart upload tasks.                                                                        |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | GetBucketAcl               | Obtains the ACL information of the bucket.                                                           |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | PutBucketAcl               | Configures the ACL for the bucket.                                                                   |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | GetBucketCORS              | Obtains the CORS configuration of the bucket.                                                        |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | PutBucketCORS              | Configures CORS for the bucket.                                                                      |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | GetBucketVersioning        | Obtains the versioning information of the bucket.                                                    |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | PutBucketVersioning        | Configures versioning for the bucket.                                                                |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | GetBucketLocation          | Obtains the bucket location.                                                                         |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | GetBucketLogging           | Obtains the bucket logging information.                                                              |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | PutBucketLogging           | Configures logging for the bucket.                                                                   |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | GetBucketWebsite           | Obtains the static website configuration information about the bucket.                               |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | PutBucketWebsite           | Configures the static website hosting for the bucket.                                                |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | DeleteBucketWebsite        | Cancels the static website hosting configuration of the bucket.                                      |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | GetLifecycleConfiguration  | Obtains the lifecycle rules of the bucket.                                                           |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+
   |         | PutLifecycleConfiguration  | Configures a lifecycle rule for the bucket.                                                          |
   +---------+----------------------------+------------------------------------------------------------------------------------------------------+

.. _obs_03_0051__section387654045518:

Actions Related to Objects
--------------------------

.. table:: **Table 2** Actions related to objects

   +---------+--------------------------+-------------------------------------------------------------------------------------------------------------+
   | Type    | Value                    | Description                                                                                                 |
   +=========+==========================+=============================================================================================================+
   | General | \*                       | The value supports a wildcard character (``*``) that indicates all operations can be performed.             |
   +---------+--------------------------+-------------------------------------------------------------------------------------------------------------+
   |         | Get\*                    | The value supports a wildcard character (``*``) that indicates all GET operations can be performed.         |
   +---------+--------------------------+-------------------------------------------------------------------------------------------------------------+
   |         | Put\*                    | The value supports a wildcard character (``*``) that indicates all PUT operations can be performed.         |
   +---------+--------------------------+-------------------------------------------------------------------------------------------------------------+
   |         | List\*                   | The value supports a wildcard character (``*``) that indicates all LIST operations can be performed.        |
   +---------+--------------------------+-------------------------------------------------------------------------------------------------------------+
   | Object  | GetObject                | Obtains the object and its metadata.                                                                        |
   +---------+--------------------------+-------------------------------------------------------------------------------------------------------------+
   |         | GetObjectVersion         | Obtains the object of a specified version and its metadata.                                                 |
   +---------+--------------------------+-------------------------------------------------------------------------------------------------------------+
   |         | PutObject                | Performs PUT upload, POST upload, multipart upload, initialization of uploaded parts, and merging of parts. |
   +---------+--------------------------+-------------------------------------------------------------------------------------------------------------+
   |         | GetObjectAcl             | Obtains the object ACL information.                                                                         |
   +---------+--------------------------+-------------------------------------------------------------------------------------------------------------+
   |         | GetObjectVersionAcl      | Obtains the ACL information of a specified object version.                                                  |
   +---------+--------------------------+-------------------------------------------------------------------------------------------------------------+
   |         | PutObjectAcl             | Configures the ACL for an object.                                                                           |
   +---------+--------------------------+-------------------------------------------------------------------------------------------------------------+
   |         | PutObjectVersionAcl      | Configures the ACL for a specified object version.                                                          |
   +---------+--------------------------+-------------------------------------------------------------------------------------------------------------+
   |         | DeleteObject             | Deletes an object.                                                                                          |
   +---------+--------------------------+-------------------------------------------------------------------------------------------------------------+
   |         | DeleteObjectVersion      | Deletes a specified object version.                                                                         |
   +---------+--------------------------+-------------------------------------------------------------------------------------------------------------+
   |         | ListMultipartUploadParts | Lists uploaded parts.                                                                                       |
   +---------+--------------------------+-------------------------------------------------------------------------------------------------------------+
   |         | AbortMultipartUpload     | Cancels a multipart upload task.                                                                            |
   +---------+--------------------------+-------------------------------------------------------------------------------------------------------------+

:original_name: en-us_topic_0125560422.html

.. _en-us_topic_0125560422:

Bucket Policy
=============

Bucket policies provide centralized, access control to buckets and objects based on a variety of conditions, including OBS operations, requesters, resources, and aspects of the request (e.g., IP address). The permissions attached to a bucket apply to all of the objects in that bucket.

Individuals as well as companies can use bucket policies. When companies register with OBS they create an *account*. Thereafter, the company becomes synonymous with the account. Accounts are financially responsible for the resources they (and their employees) create. Accounts have the power to grant bucket policy permissions and assign employees permissions based on a variety of conditions. For example, an account could create a policy that gives a user write access:

To a particular bucket

From an account's corporate network

From an account's custom application

Unlike access control lists (ACL), which can add (grant) permissions only on individual objects, policies can either add or deny permissions across all (or a subset) of objects within a bucket. With one request an account can set the permissions of any number of objects in a bucket. An account can use wildcards (similar to regular expression operators) on Amazon resource names (ARNs) and other values, so that an account can control access to groups of objects.

A bucket owner can perform the PUT Bucket policy operation to set a bucket access policy. However, a new policy will overwrite the existing one. A bucket owner can also perform the Get Bucket policy or DELETE Bucket policy operation to obtain or delete a bucket policy. After a policy is set for a bucket, all subsequent access to the bucket is controlled by the policy. Requests for accessing the bucket are accepted or denied according to the policy.

In the following example bucket policy, accounts **783fc6652cf246c096ea836694f71855** (Domain ID) and **219d520ceac84c5a98b237431a2cf4c2** (Domain ID) are granted the **GetObject** permission for all objects in **mybucket**.

.. code-block::

   {
      "Version":"2008-10-17",
      "Id":"aaaa-bbbb-cccc-dddd",
      "Statement" : [
         {
          "Effect":"Allow",
          "Sid":"1",
          "Principal" : {
            "AWS":["arn:aws:iam::783fc6652cf246c096ea836694f71855:root","arn:aws:iam::219d520ceac84c5a98b237431a2cf4c2:root"]
          },
          "Action":["s3:GetObject"],
          "Resource":"arn:aws:s3:::mybucket/*"
         }
      ]
    }

Policy Format
-------------

A policy is described in the JSON format, as shown in the following syntax:

.. code-block::

   {
    "Version" : "version",
    "Id" : "id",
    "Statement" : [statement]
    }

The **Id** and **Version** parameters are optional.

.. table:: **Table 1** Policy

   +---------+--------------------------------------------------------------------------------+----------+
   | Element | Description                                                                    | Required |
   +=========+================================================================================+==========+
   | Id      | Indicates the ID of a policy. The value is a string that describes the policy. | No       |
   +---------+--------------------------------------------------------------------------------+----------+
   | Version | Possible values are **2008-10-17**.                                            | No       |
   +---------+--------------------------------------------------------------------------------+----------+

A policy can contain multiple statements and each statement contains the following elements:

.. table:: **Table 2** statement elements

   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Element               | Description                                                                                                                                                                                                                                                                                                                                                                                                  | Required                                    |
   +=======================+==============================================================================================================================================================================================================================================================================================================================================================================================================+=============================================+
   | Sid                   | Indicates the ID of a statement. The value is a string that describes the statement.                                                                                                                                                                                                                                                                                                                         | No                                          |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Principal             | Indicates the grantee of a statement. The value can be a wildcard character (``*``) that indicates all users. When the grantee is a domain, **Principal** is in the **AWS:domainid**, **AWS:arn:aws:iam::domainid:root**, or **CanonicalUser:** format. When the grantee is a user, **Principal** is in the **AWS:arn:aws:iam::domainid:user/userId** or **AWS:arn:aws:iam::domainid:user/userName** format. | No, Choose either Principal or NotPrincipal |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                              |                                             |
   |                       | A statement grantee can specify whether the statement grantors are agency users or federated users. For agency users, the principal format is **AWS:arn:aws:iam::domainid:agency/agencyName**. For federated users, the principal format is **Federated:arn:aws:iam::domainid:identity-provider/providername** or **Federated:arn:aws:iam::domainid:group/groupname**.                                       |                                             |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | NotPrincipal          | Specifies an exception to a list of principals in the statement. You can deny access to all principals except the one named in the **NotPrincipal** element. The value of this element is similar to that of **Principal**.                                                                                                                                                                                  | No, Choose either Principal or NotPrincipal |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Action                | Specifies operations that a grantee can perform. The value is a case-insensitive string consisting of a set of operations supported by OBS.                                                                                                                                                                                                                                                                  | No, Choose either Action or NotAction       |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                              |                                             |
   |                       | The value can be a wildcard character (``*``) that indicates all operations.                                                                                                                                                                                                                                                                                                                                 |                                             |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                              |                                             |
   |                       | Example:                                                                                                                                                                                                                                                                                                                                                                                                     |                                             |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                              |                                             |
   |                       | "Action":["s3:List*", "s3:Get*"]                                                                                                                                                                                                                                                                                                                                                                             |                                             |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | NotAction             | Specifies an exception to a list of actions in the statement. All actions are performed except the one specified in **NotAction**. The value of this element is similar to **Action**.                                                                                                                                                                                                                       | No, Choose either Action or NotAction       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Effect                | Indicates whether permission in a statement is allowed or denied. The value is **Allow** or **Deny**.                                                                                                                                                                                                                                                                                                        | Yes                                         |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Resource              | Specifies resources that the statement covers. A resource is defined in the Amazon Resource Name (ARN) format. You can use a wildcard character (``*``) to represent all resources.                                                                                                                                                                                                                          | No, Choose either Resource or NotResource   |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | NotResource           | Specifies an exception to a list of resources in the statement. A policy is not applied to resources specified in **NotResource**. The value of this parameter is similar to that of **Resource**.                                                                                                                                                                                                           | No, Choose either Resource or NotResource   |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
   | Condition             | Indicates the conditions for a statement to take effect.                                                                                                                                                                                                                                                                                                                                                     | No                                          |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+

.. note::

   A statement contains either:

   -  **Action** or **NotAction**
   -  **Resource** or **NotResource**
   -  **Principal** or **NotPrincipal**

In OBS, **Action** can be the following operations on buckets:

-  s3:DeleteBucket
-  s3:ListBucket
-  s3:ListBucketVersions
-  s3:ListBucketMultipartUploads
-  s3:GetBucketAcl
-  s3:PutBucketAcl
-  s3:GetBucketCORS
-  s3:PutBucketCORS
-  s3:GetBucketVersioning
-  s3:PutBucketVersioning
-  s3:GetBucketLocation
-  s3:GetBucketLogging
-  s3:PutBucketLogging
-  s3:GetBucketWebsite
-  s3:PutBucketWebsite
-  s3:DeleteBucketWebsite
-  s3:GetLifecycleConfiguration
-  s3:PutLifecycleConfiguration
-  s3:GetBucketNotification
-  s3:PutBucketNotification
-  s3:PutBucketPolicy
-  s3:GetBucketPolicy
-  s3:DeleteBucketPolicy
-  s3:PutBucketQuota
-  s3:GetBucketQuota
-  s3:PutBucketStoragePolicy
-  s3:GetBucketStoragePolicy
-  s3:GetBucketStorage
-  s3:PutBucketTagging
-  s3:GetBucketTagging
-  s3:PutBucketObjectLockConfiguration
-  s3:GetBucketObjectLockConfiguration

In OBS, **Action** can be the following operations on objects:

-  s3:GetObject (applies to GET Object and HEAD Object)
-  s3:GetObjectVersion
-  s3:PutObject (applies to PUT Object, POST Object, Initiate Multipart Upload, Upload Part, and Complete Multipart Upload)
-  s3:GetObjectAcl
-  s3:GetObjectVersionAcl
-  s3:PutObjectAcl
-  s3:PutObjectVersionAcl
-  s3:DeleteObject
-  s3:DeleteObjectVersion
-  s3:ListMultipartUploadParts
-  s3:AbortMultipartUpload
-  s3:RestoreObject
-  s3:PutObjectRetention

OBS supports S3 resources in the ARN format:

-  arn:aws:s3:::bucketname (operations on buckets)
-  arn:aws:s3:::bucketname/path/objectname (operations on objects)

The following policy grants all permissions (including bucket and object operations) for bucket **examplebucket** to **71f3901173514e6988115ea2c26d1999** (user ID) in **b4bf1b36d9ca43d984fbcb9491b6fce9** (domain ID).

.. code-block::

   {
       "Statement":[
       {
         "Sid":"test",
         "Effect":"Allow",
         "Principal": {"AWS": ["arn:aws:iam::b4bf1b36d9ca43d984fbcb9491b6fce9:user/71f3901173514e6988115ea2c26d1999"]},
         "Action":["s3:*"],
         "Resource":[
           "arn:aws:s3:::examplebucket/*",
           "arn:aws:s3:::examplebucket"
         ]
       }
     ]
   }

or

.. code-block::

   {
       "Statement":[
       {
         "Sid":"test",
         "Effect":"Allow",
         "Principal": {"AWS": ["arn:aws:iam::b4bf1b36d9ca43d984fbcb9491b6fce9:user/user1"]},
         "Action":["s3:*"],
         "Resource":[
           "arn:aws:s3:::examplebucket/*",
           "arn:aws:s3:::examplebucket"
         ]
       }
     ]
   }

.. note::

   If you do not specify a path when uploading an object, omit **/path** in the ARN.

:ref:`Table 3 <en-us_topic_0125560422__table6811633>` lists the general types of **Condition** that you can specify.

.. _en-us_topic_0125560422__table6811633:

.. table:: **Table 3** Condition

   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type                  | Element                   | Description                                                                                                                                                               |
   +=======================+===========================+===========================================================================================================================================================================+
   | String                | StringEquals              | Strict matching                                                                                                                                                           |
   |                       |                           |                                                                                                                                                                           |
   |                       |                           | Short version: streq                                                                                                                                                      |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                       | StringNotEquals           | Strict negated matching                                                                                                                                                   |
   |                       |                           |                                                                                                                                                                           |
   |                       |                           | Short version: strneq                                                                                                                                                     |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                       | StringEqualsIgnoreCase    | Strict matching, ignoring case                                                                                                                                            |
   |                       |                           |                                                                                                                                                                           |
   |                       |                           | Short version: streqi                                                                                                                                                     |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                       | StringNotEqualsIgnoreCase | Strict negated matching, ignoring case                                                                                                                                    |
   |                       |                           |                                                                                                                                                                           |
   |                       |                           | Short version: strneqi                                                                                                                                                    |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                       | StringLike                | Loose case-insensitive matching. The values can include a multi-character match wildcard (``*``) or a single-character match wildcard (?) anywhere in the string.         |
   |                       |                           |                                                                                                                                                                           |
   |                       |                           | Short version: strl                                                                                                                                                       |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                       | StringNotLike             | Negated loose case-insensitive matching. The values can include a multi-character match wildcard (``*``) or a single-character match wildcard (?) anywhere in the string. |
   |                       |                           |                                                                                                                                                                           |
   |                       |                           | Short version: strnl                                                                                                                                                      |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Numeric               | NumericEquals             | Strict matching                                                                                                                                                           |
   |                       |                           |                                                                                                                                                                           |
   |                       |                           | Short version: numeq                                                                                                                                                      |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                       | NumericNotEquals          | Strict negated matching                                                                                                                                                   |
   |                       |                           |                                                                                                                                                                           |
   |                       |                           | Short version: numneq                                                                                                                                                     |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                       | NumericLessThan           | "Less than" matching                                                                                                                                                      |
   |                       |                           |                                                                                                                                                                           |
   |                       |                           | Short version: numlt                                                                                                                                                      |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                       | NumericLessThanEquals     | "Less than or equals" matching                                                                                                                                            |
   |                       |                           |                                                                                                                                                                           |
   |                       |                           | Short version: numlteq                                                                                                                                                    |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                       | NumericGreaterThan        | "Greater than" matching                                                                                                                                                   |
   |                       |                           |                                                                                                                                                                           |
   |                       |                           | Short version: numgt                                                                                                                                                      |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                       | NumericGreaterThanEquals  | "Greater than or equals" matching                                                                                                                                         |
   |                       |                           |                                                                                                                                                                           |
   |                       |                           | Short version: numgteq                                                                                                                                                    |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Date                  | DateEquals                | Strict matching                                                                                                                                                           |
   |                       |                           |                                                                                                                                                                           |
   |                       |                           | Short version: dateeq                                                                                                                                                     |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                       | DateNotEquals             | Strict negated matching                                                                                                                                                   |
   |                       |                           |                                                                                                                                                                           |
   |                       |                           | Short version: dateneq                                                                                                                                                    |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                       | DateLessThan              | A point in time at which a key stops taking effect                                                                                                                        |
   |                       |                           |                                                                                                                                                                           |
   |                       |                           | Short version: datelt                                                                                                                                                     |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                       | DateLessThanEquals        | A point in time at which a key stops taking effect                                                                                                                        |
   |                       |                           |                                                                                                                                                                           |
   |                       |                           | Short version: datelteq                                                                                                                                                   |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                       | DateGreaterThan           | A point in time at which a key starts to take effect                                                                                                                      |
   |                       |                           |                                                                                                                                                                           |
   |                       |                           | Short version: dategt                                                                                                                                                     |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                       | DateGreaterThanEquals     | A point in time at which a key starts to take effect                                                                                                                      |
   |                       |                           |                                                                                                                                                                           |
   |                       |                           | Short version: dategteq                                                                                                                                                   |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Boolean               | Bool                      | Strict Boolean matching                                                                                                                                                   |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | IP address            | IpAddress                 | Approved based on the IP address or range                                                                                                                                 |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                       | NotIpAddress              | Denial based on the IP address or range                                                                                                                                   |
   +-----------------------+---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   Elements in **Condition** are case-sensitive. Date conditions must be in the ISO 8601 format. For details, see http://www.w3.org/TR/NOTE-datetime.

A **Condition** block (element) can contain multiple key value pairs. The following example **Condition** block specifies requests initiated between 2009-04-16T12:00:00Z and 2009-04-16T15:00:00Z from IP addresses on network segment 192.168.176.0/24 or 192.168.143.0/24:

.. code-block::

   "Condition" : {
       "DateGreaterThan": {
           "aws:CurrentTime" : "2009-04-16T12:00:00Z"
       },
       "DateLessThan": {
           "aws:CurrentTime" : "2009-04-16T15:00:00Z"
       },
       "IpAddress": {
           "aws:SourceIp" : ["192.168.176.0/24", "192.168.143.0/24"]
       }
    }

A **Condition** block can contain two types of keys:

-  General keys that have nothing to do with **Action**.
-  S3 service-specific keys associated with **Action**.

:ref:`Table 4 <en-us_topic_0125560422__table61304705>` lists the general keys.

.. _en-us_topic_0125560422__table61304705:

.. table:: **Table 4** Common Condition Key

   =================== ==============
   Condition Key       Condition Type
   =================== ==============
   aws:CurrentTime     Date
   aws:EpochTime       Numeric
   aws:SecureTransport Boolean
   aws:SourceIp        IP address
   aws:UserAgent       String
   aws:Referer         String
   =================== ==============

:ref:`Table 5 <en-us_topic_0125560422__table14871440>` lists the OBS service-specific keys.

.. _en-us_topic_0125560422__table14871440:

.. table:: **Table 5** OBS Action Condition Key

   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | Action                             | Key                       | Description                                                                                                                               |
   +====================================+===========================+===========================================================================================================================================+
   | s3:CreateBucket                    | s3:x-amz-acl              | **x-amz-acl** can contain the canned ACL.                                                                                                 |
   |                                    |                           |                                                                                                                                           |
   |                                    |                           | Valid values: private\| public-read\| public-read-write|authenticated-read|bucket-owner-read|bucket-owner-full-control|log-delivery-write |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   |                                    | s3:x-amz-grant-permission | Not supported                                                                                                                             |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   |                                    | s3:LocationConstraint     | Not supported                                                                                                                             |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | s3:ListBucket                      | s3:prefix                 | String                                                                                                                                    |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   |                                    | s3:delimiter              | String                                                                                                                                    |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   |                                    | s3:max-keys               | Numeric                                                                                                                                   |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | s3:ListBucketVersions              | s3:prefix                 | String                                                                                                                                    |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   |                                    | s3:delimiter              | String                                                                                                                                    |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   |                                    | s3:max-keys               | Numeric                                                                                                                                   |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | s3:PutBucketAcl                    | s3:x-amz-acl              | **x-amz-acl** can contain the canned ACL.                                                                                                 |
   |                                    |                           |                                                                                                                                           |
   |                                    |                           | Valid values: private\| public-read\| public-read-write|authenticated-read|bucket-owner-read|bucket-owner-full-control|log-delivery-write |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   |                                    | s3:x-amz-grant-permission | Not supported                                                                                                                             |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | s3:PutObject                       | s3:x-amz-acl              | **x-amz-acl** can contain the canned ACL.                                                                                                 |
   |                                    |                           |                                                                                                                                           |
   |                                    |                           | Valid values: private\| public-read\| public-read-write|authenticated-read|bucket-owner-read|bucket-owner-full-control|log-delivery-write |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   |                                    | s3:x-amz-copy-source      | String                                                                                                                                    |
   |                                    |                           |                                                                                                                                           |
   |                                    |                           | Example format:                                                                                                                           |
   |                                    |                           |                                                                                                                                           |
   |                                    |                           | **/bucketname/keyname**                                                                                                                   |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   |                                    | s3:x-amz-metadata-di      | Valid values: COPY\| REPLACE                                                                                                              |
   |                                    |                           |                                                                                                                                           |
   |                                    | rective                   |                                                                                                                                           |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   |                                    | s3:x-amz-grant-permission | Not supported                                                                                                                             |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   |                                    | s3:x-amz-storage-class    | Not supported                                                                                                                             |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | s3:PutObjectAcl                    | s3:x-amz-acl              | **x-amz-acl** can contain the canned ACL.                                                                                                 |
   |                                    |                           |                                                                                                                                           |
   |                                    |                           | Valid values: private\| public-read\| public-read-write|authenticated-read|bucket-owner-read|bucket-owner-full-control|log-delivery-write |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   |                                    | s3:x-amz-grant-permission | Not supported                                                                                                                             |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | s3:GetObjectVersion                | s3:VersionId              | String                                                                                                                                    |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | s3:GetObjectVersionAcl             | s3:VersionId              | String                                                                                                                                    |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | s3:PutObjectVersionAcl             | s3:VersionId              | String                                                                                                                                    |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   |                                    | s3:x-amz-acl              | **x-amz-acl** can contain the canned ACL.                                                                                                 |
   |                                    |                           |                                                                                                                                           |
   |                                    |                           | Valid values: private\| public-read\| public-read-write|authenticated-read|bucket-owner-read|bucket-owner-full-control|log-delivery-write |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   |                                    | s3:x-amz-grant-permission | Not supported                                                                                                                             |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | s3:DeleteObjectVersion             | s3:VersionId              | String                                                                                                                                    |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | s3:\*                              | s3:signatureversion       | Not supported                                                                                                                             |
   |                                    |                           |                                                                                                                                           |
   | (Actions or any of the S3 Actions) |                           |                                                                                                                                           |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   |                                    | s3:authType               | Not supported                                                                                                                             |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   |                                    | s3:signatureAge           | Not supported                                                                                                                             |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   |                                    | s3:x-amz-content-sha256   | Not supported                                                                                                                             |
   +------------------------------------+---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+

Policy Permission Judgment Logic
--------------------------------

A policy results in a default deny if conditions in any statement of the policy are not met. If all conditions in statements are met, the policy results in either an allow or an explicit deny. If a bucket policy contains multiple statements, the policy determines which statement prevails according to the following rules:

1. If conditions in any statement of a policy are not met, the policy results in a default deny.

2. An explicit deny overrides allows.

3. An allow overrides default denies.

4. Statements can be in any order in a policy.

.. table:: **Table 6** Statement results

   +-----------------------------------+--------------------------------------------------------------------------------------------------+
   | Name                              | Description                                                                                      |
   +===================================+==================================================================================================+
   | explicit deny                     | A statement defines effect="deny".                                                               |
   |                                   |                                                                                                  |
   |                                   | All requests for resources to which the statement applies are denied. No permission is returned. |
   +-----------------------------------+--------------------------------------------------------------------------------------------------+
   | allow                             | A statement defines effect="allow".                                                              |
   |                                   |                                                                                                  |
   |                                   | All requests for resources to which the statement applies are allowed.                           |
   +-----------------------------------+--------------------------------------------------------------------------------------------------+
   | default deny                      | Conditions defined in a statement are not met. Requests are denied.                              |
   +-----------------------------------+--------------------------------------------------------------------------------------------------+

URL Validation Settings
-----------------------

OBS is charged based on the services that you use. To prevent user data from being stolen, OBS supports URL validation based on HTTP headers. OBS also supports both whitelist and blacklist settings.

-  Whitelist settings

   Users can set a whitelist to allow requests from the websites added in the whitelist and deny requests from any other website.

   For the requests that are initialized from browsers' address boxes, that is, those HTTP requests with a blank **referer**, users can add the **${null}** field to **"aws:Referer"** of **Condition** to specify whether to allow the requests with a blank **referer**.

   Set a whitelist based on the following policy setting:

   .. code-block::

      "Statement": [
          {"Sid": "1",
           "Effect": "Allow",
           "Principal": {"CanonicalUser":["*"]},
           "Action": "s3:*",
           "Resource":["arn:aws:s3:::bucket/*"],
          },
          {"Sid": "2",
           "Effect": "Deny",
           "Principal":{"CanonicalUser":["*"]},
           "Action": ["s3:*"],
           "Resource": ["arn:aws:s3:::bucket/*"],
           "Condition":{
               "StringNotEquals":{
                    "aws:Referer": ["www.example01.com","${null}"]
                   }
               }
           }
      ]

   If you set a whitelist in this way, you can perform operations on resources in buckets only when the value of the **referer** parameter is **www.example01.com** or is blank.

-  Blacklist settings

   You can refer to the following policy settings to set a blacklist for access.

   .. code-block::

      "Statement": [
          {"Sid":"1",
           "Effect":"Deny",
           "Principal":{"CanonicalUser":["*"]},
           "Action":["s3: *"],
           "Resource":["arn:aws:s3:::bucket/*"],
           "Condition":{
               "StringEquals":{
                   "aws:Referer":["www.example01.com", "www.example02.com"]
                   }
               }
           }
       ]

   If you set a blacklist in this way, you cannot perform operations on resources in buckets when the value of the **referer** parameter is **www.example01.com** or **www.example02.com**.

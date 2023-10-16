:original_name: obs_04_0098.html

.. _obs_04_0098:

Initiating a Multipart Upload
=============================

Functions
---------

Before using this operation, make an API operation call to create a multipart upload task. The system will return a globally unique upload ID as the multipart upload identifier. This identifier can be used in subsequent requests including UploadPart, CompleteMultipartUpload, and ListParts. Create a multipart upload task does not affect the object that has the same name as object to be uploaded in multiple parts. You can create more than one multipart upload tasks for an object. This operation request can contain headers **x-obs-acl**, **x-obs-meta-\***, **Content-Type**, and **Content-Encoding**. The headers are recorded in the multipart upload metadata.

WORM
----

If a bucket has WORM enabled, you can configure object-level retention policies when initiating multipart uploads. You can specify the **x-obs-object-lock-mode** and **x-obs-object-lock-retain-until-date** headers when you initiate a multipart upload to protect the object assembled. If you do not specify these two headers but have configured a default bucket-level WORM policy, this default policy automatically applies to the object newly assembled. You can also configure or update a WORM retention policy after the object is assembled.

Different from uploads with PUT and POST, a multipart upload only requires that the date specified in the **x-obs-object-lock-retain-until-date** header be no later than the initiation time, but does not have to be later than the completion time of the multipart upload. When the default bucket-level WORM policy is applied, the protection starts when the object parts are assembled and ends once the default bucket-level protection period expires. Before assembling the object parts uploaded, the multipart upload can be canceled and will not be affected by the WORM configuration.

Request Syntax
--------------

.. code-block:: text

   POST /ObjectName?uploads  HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization

Request Parameters
------------------

This request uses parameters to specify a multipart upload. :ref:`Table 1 <obs_04_0098__table13291134>` describes the parameters.

.. _obs_04_0098__table13291134:

.. table:: **Table 1** Request parameters

   +-----------------------+-------------------------------+-----------------------+
   | Parameter             | Description                   | Mandatory             |
   +=======================+===============================+=======================+
   | uploads               | Indicates a multipart upload. | Yes                   |
   |                       |                               |                       |
   |                       | Type: string                  |                       |
   +-----------------------+-------------------------------+-----------------------+

Request Headers
---------------

The request can use additional headers, as shown in :ref:`Table 2 <obs_04_0098__table11912770163049>`.

.. _obs_04_0098__table11912770163049:

.. table:: **Table 2** Request headers

   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | Header                              | Description                                                                                                                                                                                                                                                                     | Mandatory                                                                 |
   +=====================================+=================================================================================================================================================================================================================================================================================+===========================================================================+
   | x-obs-acl                           | When initiating a multipart upload, you can add this message header to set the permission control policy for the object. The predefined common policies are as follows: **private**, **public-read**, and **public-read-write**.                                                | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Note: This header is a predefined policy expressed in a character string.                                                                                                                                                                                                       |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-acl: public-read-write**                                                                                                                                                                                                                                       |                                                                           |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-grant-read                    | When initiating a multipart upload, you can use this header to grant all users in an account the permissions to read the object and obtain the object metadata.                                                                                                                 | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-grant-read: ID=domainID** If multiple accounts are authorized, separate them with commas (,).                                                                                                                                                                  |                                                                           |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-grant-read-acp                | When initiating a multipart upload, you can use this header to grant all users in an account the permission to obtain the object ACL.                                                                                                                                           | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-grant-read-acp: ID=domainID** If multiple accounts are authorized, separate them with commas (,).                                                                                                                                                              |                                                                           |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-grant-write-acp               | When initiating a multipart upload, you can use this header to grant all users in an account the permission to write the object ACL.                                                                                                                                            | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-grant-write-acp: ID=domainID** If multiple accounts are authorized, separate them with commas (,).                                                                                                                                                             |                                                                           |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-grant-full-control            | When initiating a multipart upload, you can use this header to grant all users in an account the permissions to read the object, obtain the object metadata and ACL, and write the object ACL.                                                                                  | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-grant-full-control: ID=domainID** If multiple accounts are authorized, separate them with commas (,).                                                                                                                                                          |                                                                           |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-website-redirect-location     | If a bucket is configured with the static website hosting function, it will redirect requests for this object to another object in the same bucket or to an external URL. OBS stores the value of this header in the object metadata.                                           | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Default value: none                                                                                                                                                                                                                                                             |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Constraint: The value must be prefixed by a slash (/), **http://**, or **https://**. The length of the value cannot exceed 2 KB.                                                                                                                                                |                                                                           |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-expires                       | Specifies when an object expires. It is measured in days. Once the object expires, it is automatically deleted. (The calculation starts from when the object was last modified).                                                                                                | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: integer                                                                                                                                                                                                                                                                   |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-expires:3**                                                                                                                                                                                                                                                    |                                                                           |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-object-lock-mode              | WORM mode that will be applied to the object. Currently, only **COMPLIANCE** is supported. This header must be used together with **x-obs-object-lock-retain-until-date**.                                                                                                      | No, but required when **x-obs-object-lock-retain-until-date** is present. |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-object-lock-mode:COMPLIANCE**                                                                                                                                                                                                                                  |                                                                           |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-object-lock-retain-until-date | Indicates the expiration time of the Object Lock retention. The value must be a UTC time that complies with ISO 8601, for example, **2015-07-01T04:11:15Z**. This header must be used together with **x-obs-object-lock-mode**.                                                 | No, but required when **x-obs-object-lock-mode** is present.              |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-object-lock-retain-until-date:2015-07-01T04:11:15Z**                                                                                                                                                                                                           |                                                                           |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | x-obs-meta-\*                       | When initiating a multipart upload, you can use a header starting with **x-obs-meta-** in the HTTP request to define object metadata for easy management. The user-defined metadata will be returned in the response when you retrieve the object or query the object metadata. | No                                                                        |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Type: string                                                                                                                                                                                                                                                                    |                                                                           |
   |                                     |                                                                                                                                                                                                                                                                                 |                                                                           |
   |                                     | Example: **x-obs-meta-test: test metadata**                                                                                                                                                                                                                                     |                                                                           |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+

For details about other common message headers, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Request Elements
----------------

This request involves no elements.

Response Syntax
---------------

::

   HTTP/1.1 status_code
   Date: date
   Content-Length: length
   Connection: status

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <InitiateMultipartUploadResult xmlns="http://obs.region.example.com/doc/2015-06-30/">
       <Bucket>BucketName</Bucket>
       <Key>ObjectName</Key>
       <UploadId>uploadID</UploadId>
   </InitiateMultipartUploadResult>

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains elements to indicate the upload ID and the key (name) of the object (bucket) for which the multipart upload was initiated. The returned information is used in the subsequent operations. :ref:`Table 3 <obs_04_0098__table6651816>` describes the elements.

.. _obs_04_0098__table6651816:

.. table:: **Table 3** Response elements

   +-----------------------------------+----------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                        |
   +===================================+====================================================================================================+
   | InitiateMultipartUploadResult     | Container of a multipart upload task.                                                              |
   |                                   |                                                                                                    |
   |                                   | Type: XML                                                                                          |
   +-----------------------------------+----------------------------------------------------------------------------------------------------+
   | Bucket                            | Indicates the name of the bucket to which the multipart upload was initiated.                      |
   |                                   |                                                                                                    |
   |                                   | Type: string                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------+
   | Key                               | Indicates the object key in a multipart upload.                                                    |
   |                                   |                                                                                                    |
   |                                   | Type: string                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------+
   | UploadId                          | Indicates the ID for the initiated multipart upload. This ID is used for the subsequent operation. |
   |                                   |                                                                                                    |
   |                                   | Type: string                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------+

Error Responses
---------------

1. If the AK or signature is invalid, OBS returns **403 Forbidden** and the error code is **AccessDenied**.

2. If the bucket is not found, OBS returns **404 Not Found** and the error code is **NoSuchBucket**.

3. Check whether the user has the write permission for the specified bucket. If no, OBS returns **403 Forbidden** and the error code is **AccessDenied**.

Other errors are included in :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request: Initiating a Multipart Upload
---------------------------------------------

.. code-block:: text

   POST /objectkey?uploads  HTTP/1.1
   Host: examplebucket.obs.region.example.com
   Date: WED, 01 Jul 2015 05:14:52 GMT
   Authorization: OBS AKIAIOSFODNN7EXAMPLE:VGhpcyBtZXNzYWdlIHNpZ25lZGGieSRlbHZpbmc=

Sample Response: Initiating a Multipart Upload
----------------------------------------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-id-2: Weag1LuByRx9e6j5Onimru9pO4ZVKnJ2Qz7/C1NPcfTWAtRPfTaOFg==
   x-obs-request-id: 996c76696e6727732072657175657374
   Date: WED, 01 Jul 2015 05:14:52 GMT
   Content-Length: 303

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <InitiateMultipartUploadResult xmlns="http://obs.region.example.com/doc/2015-06-30/">
     <Bucket>bucketname</Bucket>
     <Key>objectkey</Key>
     <UploadId>DCD2FC98B4F70000013DF578ACA318E7</UploadId>
   </InitiateMultipartUploadResult>

Sample Request: Initiating a Multipart Upload (with the ACL Configured)
-----------------------------------------------------------------------

.. code-block:: text

   POST /objectkey?uploads  HTTP/1.1
   Host: examplebucket.obs.region.example.com
   Date: WED, 01 Jul 2015 05:15:43 GMT
   x-obs-grant-write-acp:ID=52f24s3593as5730ea4f722483579ai7,ID=a93fcas852f24s3596ea8366794f7224
   Authorization: OBS AKIAIOSFODNN7EXAMPLE:VGhpcyBtZXNzYWdlIHNpZ25lZGGieSRlbHZpbmc=

Sample Response: Initiating a Multipart Upload (with the ACL Configured)
------------------------------------------------------------------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCTnv+daB51p+IVhAvWN7s5rSKhcWqDFs
   x-obs-request-id: BB78000001648457112DF37FDFADD7AD
   Date: WED, 01 Jul 2015 05:15:43 GMT
   Content-Length: 303

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <InitiateMultipartUploadResult xmlns="http://obs.region.example.com/doc/2015-06-30/">
     <Bucket>bucketname</Bucket>
     <Key>objectkey</Key>
     <UploadId>000001648453845DBB78F2340DD460D8</UploadId>
   </InitiateMultipartUploadResult>

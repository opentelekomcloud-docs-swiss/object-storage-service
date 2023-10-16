:original_name: obs_04_0034.html

.. _obs_04_0034:

Configuring Bucket Lifecycle Rules
==================================

Functions
---------

This operation configures lifecycle rules that can delete objects from a bucket at a specified time. Typical application scenarios:

-  Delete periodically uploaded files. Some files uploaded periodically need only to be retained for only one week or one month.
-  Delete files that are frequently accessed within a certain period of time but are seldom accessed afterward. You can archive these files and then schedule the time for deletion.

You can perform this operation to create or update the lifecycle configuration of a bucket.

.. note::

   -  Expired objects deleted based on a lifecycle rule cannot be recovered.

To perform this operation, you must have the **PutLifecycleConfiguration** permission. By default, only the bucket owner can perform this operation. The bucket owner can grant the permission to other users by configuring the bucket policy or user policy.

The lifecycle configuration enables OBS to delete objects at a scheduled time. To prevent a user from doing so, the following permissions granted to the user must be revoked:

-  DeleteObject
-  DeleteObjectVersion
-  PutLifecycleConfiguration

If you want to forbid a user to set the bucket lifecycle configuration, revoke the **PutLifecycleConfiguration** permission from the user.

Request Syntax
--------------

.. code-block:: text

   PUT /?lifecycle HTTP/1.1
   Host: bucketname.obs.region.example.com
   Content-Length: length
   Date: date
   Authorization: authorization
   Content-MD5: MD5
   <?xml version="1.0" encoding="UTF-8"?>
   <LifecycleConfiguration>
       <Rule>
           <ID>id</ID>
           <Prefix>prefix</Prefix>
           <Status>status</Status>
           <Expiration>
               <Days>days</Days>
           </Expiration>
           <NoncurrentVersionExpiration>
               <NoncurrentDays>days</NoncurrentDays>
           </NoncurrentVersionExpiration>
       </Rule>
   </LifecycleConfiguration>

Request Parameters
------------------

This request contains no message parameters.

Request Headers
---------------

:ref:`Table 1 <obs_04_0034__table436706591789>` lists the request header.

.. _obs_04_0034__table436706591789:

.. table:: **Table 1** Request headers

   +-----------------------+-------------------------------------------------------------------------+-----------------------+
   | Header                | Description                                                             | Mandatory             |
   +=======================+=========================================================================+=======================+
   | Content-MD5           | Base64-encoded 128-bit MD5 digest of the message according to RFC 1864. | Yes                   |
   |                       |                                                                         |                       |
   |                       | Type: string                                                            |                       |
   |                       |                                                                         |                       |
   |                       | Example: **n58IG6hfM7vqI4K0vnWpog==**                                   |                       |
   +-----------------------+-------------------------------------------------------------------------+-----------------------+

Request Elements
----------------

In this request, you need to specify the lifecycle configuration in the request body. The lifecycle configuration can be uploaded in the form of an XML file with elements described in :ref:`Table 2 <obs_04_0034__table49391898171726>`.

-  If the versioning of a bucket is enabled or suspended, you can set **NoncurrentVersionExpiration** to control the lifecycle of historical object versions. The lifecycle of a historical version depends on the time when it becomes a historical one (time when the version is replaced by a new version) and the value of **NoncurrentDays**. , if **NoncurrentDays** is set to **1**, an object version will be deleted only after it becomes a historical one for one day. If the version V1 of object A is created on the first date of a month and new version V2 is uploaded on the fifth date of the month, V1 becomes a historical version. At 00:00 on the seventh date of the month, V1 will expire. The deletion of the object after the expiration time may be delayed. The delay is within 48 hours.
-  Objects are processed according to the following procedures, if their latest versions meet the expiration rule and versioning is enabled or suspended for the bucket.

   -  Versioning enabled:

      If the latest object version is not a delete marker, a new delete marker will be inserted for the object.

      If the latest object version is a delete marker and is the only version of the object, this latest version will be deleted.

      If the object of the latest version has the DeleteMarker and the object has other versions, all versions of the object remain unchanged.

   -  Versioning suspended:

      If the latest version of the object does not have the DeleteMarker and is not the null version, the object generates a new DeleteMarker for the null version.

      If the latest version of the object does not have the DeleteMarker but is the null version, this null version is overwritten by a new DeleteMarker generated for the null version.

      If the latest object version is a delete marker and is the only version of the object, this latest version will be deleted.

      If the object of the latest version has the DeleteMarker and the object has other versions, all versions of the object remain unchanged.

.. _obs_04_0034__table49391898171726:

.. table:: **Table 2** Response elements for lifecycle configuration

   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | Name                        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Mandatory                                                           |
   +=============================+===================================================================================================================================================================================================================================================================================================================================================================================================================================================================+=====================================================================+
   | Date                        | Specifies that OBS executes lifecycle rules for objects before the specified date. The date must be compliant with the ISO8601 format, and the time must be compliant with the UTC format of 00:00:00. For example, **2018-01-01T00:00:00.000Z** indicates that objects whose last modification time is earlier than **2018-01-01T00:00:00.000Z** are deleted. Objects whose last modification time is equal to or later than the specified time are not deleted. | Required if the **Days** element is absent.                         |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Type: string                                                                                                                                                                                                                                                                                                                                                                                                                                                      |                                                                     |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Ancestor node: Expiration                                                                                                                                                                                                                                                                                                                                                                                                                                         |                                                                     |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | Days                        | Specifies the number of days (since the latest update to the latest object version) after which the lifecycle rule takes effect.                                                                                                                                                                                                                                                                                                                                  | Required if the **Date** element is absent.                         |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Type: integer                                                                                                                                                                                                                                                                                                                                                                                                                                                     |                                                                     |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Ancestor node: Expiration                                                                                                                                                                                                                                                                                                                                                                                                                                         |                                                                     |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | Expiration                  | Container for the object expiration rule (only applicable to the latest versions of objects).                                                                                                                                                                                                                                                                                                                                                                     | Yes                                                                 |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Type: XML                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                                                                     |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Children node: Date or Days                                                                                                                                                                                                                                                                                                                                                                                                                                       |                                                                     |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Ancestor node: Rule                                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                     |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | ID                          | Unique identifier of a rule. The value can contain a maximum of 255 characters.                                                                                                                                                                                                                                                                                                                                                                                   | No                                                                  |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Type: string                                                                                                                                                                                                                                                                                                                                                                                                                                                      |                                                                     |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Ancestor node: Rule                                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                     |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | LifecycleConfiguration      | Container for lifecycle rules. You can add multiple rules. The total size of the rules cannot exceed 20 KB.                                                                                                                                                                                                                                                                                                                                                       | Yes                                                                 |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Type: XML                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                                                                     |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Children node: Rule                                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                     |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Ancestor node: none                                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                     |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | NoncurrentDays              | Number of days when the specified rule takes effect after the object becomes a historical version (only applicable to an object's historical version).                                                                                                                                                                                                                                                                                                            | Required if the **NoncurrentVersionExpiration** element is present. |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Type: integer                                                                                                                                                                                                                                                                                                                                                                                                                                                     |                                                                     |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Ancestor node: NoncurrentVersionExpiration                                                                                                                                                                                                                                                                                                                                                                                                                        |                                                                     |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | NoncurrentVersionExpiration | Container for the expiration time of objects' historical versions. If versioning is enabled or suspended for a bucket, you can set **NoncurrentVersionExpiration** to delete historical versions of objects that match the lifecycle rule (only applicable to the historical versions of objects).                                                                                                                                                                | No                                                                  |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Type: XML                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                                                                     |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Children node: NoncurrentDays                                                                                                                                                                                                                                                                                                                                                                                                                                     |                                                                     |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Ancestor node: Rule                                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                     |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | Prefix                      | Object name prefix that identifies one or more objects to which the rule applies.                                                                                                                                                                                                                                                                                                                                                                                 | Yes                                                                 |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Type: string                                                                                                                                                                                                                                                                                                                                                                                                                                                      |                                                                     |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Ancestor node: Rule                                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                     |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Constraints:                                                                                                                                                                                                                                                                                                                                                                                                                                                      |                                                                     |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | #. When you configure a lifecycle rule by specifying a prefix, if the specified prefix and the prefix of an existing lifecycle rule overlap, OBS regards these two rules as one and forbids you to configure this rule. For example, if there is a rule with the object prefix **abc** configured in the system, another rule with the object prefix starting with **abc** cannot be configured.                                                                  |                                                                     |
   |                             | #. If there is already a lifecycle rule that is based on an object prefix, you are not allowed to configure another rule that is applied to the entire bucket.                                                                                                                                                                                                                                                                                                    |                                                                     |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | Rule                        | Container for a specific lifecycle rule.                                                                                                                                                                                                                                                                                                                                                                                                                          | Yes                                                                 |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Type: container                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Ancestor node: LifecycleConfiguration                                                                                                                                                                                                                                                                                                                                                                                                                             |                                                                     |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | Status                      | Indicates whether the rule is enabled.                                                                                                                                                                                                                                                                                                                                                                                                                            | Yes                                                                 |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Type: string                                                                                                                                                                                                                                                                                                                                                                                                                                                      |                                                                     |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Ancestor node: Rule                                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                     |
   |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                     |
   |                             | Value options: **Enabled**, **Disabled**                                                                                                                                                                                                                                                                                                                                                                                                                          |                                                                     |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+

Response Syntax
---------------

::

   HTTP/1.1 status_code
   Date: date
   Content-Length: length

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   PUT /?lifecycle HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 03:05:34 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:DpSAlmLX/BTdjxU5HOEwflhM0WI=
   Content-MD5: ujCZn5p3fmczNiQQxdsGaQ==
   Content-Length: 919

   <?xml version="1.0" encoding="utf-8"?>
   <LifecycleConfiguration>
     <Rule>
       <ID>delete-2-days</ID>
       <Prefix>test/</Prefix>
       <Status>Enabled</Status>
       <Expiration>
         <Days>70</Days>
       </Expiration>
       <NoncurrentVersionExpiration>
         <NoncurrentDays>70</NoncurrentDays>
       </NoncurrentVersionExpiration>
     </Rule>
   </LifecycleConfiguration>

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF26000001643670AC06E7B9A7767921
   x-obs-id-2: 32AAAQAAEAABSAAgAAEAABAAAQAAEAABCSvK6z8HV6nrJh49gsB5vqzpgtohkiFm
   Date: WED, 01 Jul 2015 03:05:34 GMT
   Content-Length: 0

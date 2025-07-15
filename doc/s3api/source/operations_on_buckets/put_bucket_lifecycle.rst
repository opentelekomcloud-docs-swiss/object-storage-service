:original_name: en-us_topic_0125560423.html

.. _en-us_topic_0125560423:

PUT Bucket lifecycle
====================

OBS supports periodic transition and deletion of objects in a bucket based on a specified rule. This is implemented in lifecycle configuration. After the bucket lifecycle is set, OBS automatically deletes objects at the time specified in this operation. This operation can be used to delete:

-  Periodically uploaded files: Some periodically uploaded files need to be retained for only one week or one month.
-  Documents that are seldom accessed after a certain period of time. These documents may be archived for another period of time and be deleted then.

This operation is used to create or update the lifecycle configuration of a bucket.

Only users granted the **s3:PutLifecycleConfiguration** permission can create or update the bucket lifecycle configuration. By default, only the bucket owner can set the bucket lifecycle configuration. The bucket owner can allow other users to set the bucket lifecycle configuration by granting them the permission.

The lifecycle configuration supports periodic deletion and transition of objects. If you want to prevent a user from deleting and transitioning objects, disable the following permissions:

-  s3:DeleteObject
-  s3:DeleteObjectVersion
-  s3:PutLifecycleConfiguration

If you want to prevent a user configuring a bucket lifecycle, revoke the **s3:PutLifecycleConfiguration** permission from the user.

Request Syntax
--------------

.. code-block:: text

   PUT /?lifecycle HTTP/1.1
   User-Agent: user-agent
   Host: bucketname.obs.example.com
   Content-Length: length
   Date: date
   Authorization: authorization
   Content-MD5: MD5
   Expect: expect

   <?xml version="1.0" encoding="UTF-8"?>
   <LifecycleConfiguration>
    <Rule>
     <ID>id</ID>
     <Prefix>prefix</Prefix>
     <Status>status</Status>
     <Expiration>
      <Days>365</Days>
     </Expiration>
     <NoncurrentVersionExpiration>
      <NoncurrentDays>365</NoncurrentDays>
     </NoncurrentVersionExpiration>
     <Transition>
      <Days>30</Days>
      <StorageClass>STANDARD_IA</StorageClass>
     </Transition>
     <Transition>
      <Days>60</Days>
      <StorageClass>GLACIER</StorageClass>
     </Transition>
     <NoncurrentVersionTransition>
      <NoncurrentDays>30</NoncurrentDays>
      <StorageClass>STANDARD_IA</StorageClass>
     </NoncurrentVersionTransition>
     <NoncurrentVersionTransition>
      <NoncurrentDays>60</NoncurrentDays>
      <StorageClass>GLACIER</StorageClass>
     </NoncurrentVersionTransition>
     <AbortIncompleteMultipartUpload>
      <DaysAfterInitiation>10</DaysAfterInitiation>
     </AbortIncompleteMultipartUpload>
    </Rule>
   </LifecycleConfiguration>

Request Parameters
------------------

This request involves no parameters.

Request Headers
---------------

The request uses one header, as described in :ref:`Table 1 <en-us_topic_0125560423__table16725372>`.

.. _en-us_topic_0125560423__table16725372:

.. table:: **Table 1** Request header

   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | Header                | Description                                                                                                                                                                                                                                                                 | Remarks                                                                          |
   +=======================+=============================================================================================================================================================================================================================================================================+==================================================================================+
   | Content-MD5           | The MD5 digest string of the message body is calculated according to the RFC 1864 standard. That is, calculate the 128-bit binary array (the message header data encrypted with MD5) first, and then use Base 64 encoding to convert the binary data to a character string. | Mandatory                                                                        |
   |                       |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                       | Type: String                                                                                                                                                                                                                                                                |                                                                                  |
   |                       |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                       | Example: n58IG6hfM7vqI4K0vnWpog==                                                                                                                                                                                                                                           |                                                                                  |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-security-token  | Header field used to identify the request of a federated user. When the federal authentication function is enabled, users sending such requests are identified as federated users.                                                                                          | Optional. This parameter must be carried in the request sent by federated users. |
   |                       |                                                                                                                                                                                                                                                                             |                                                                                  |
   |                       | Type: string                                                                                                                                                                                                                                                                |                                                                                  |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+

Request Elements
----------------

In this request, you need to specify the lifecycle configuration in the request body using the elements described in :ref:`Table 2 <en-us_topic_0125560423__table26371793>`.

.. _en-us_topic_0125560423__table26371793:

.. table:: **Table 2** Request elements for lifecycle configuration

   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | Element                        | Description                                                                                                                                                                                                                                                 | Remarks                                                                                                                                           |
   +================================+=============================================================================================================================================================================================================================================================+===================================================================================================================================================+
   | Date                           | Indicates when the specified rule takes effect (applicable to the latest object version).                                                                                                                                                                   | Mandatory if the **Days** parameter is absent.                                                                                                    |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | The date value must conform to ISO 8601 format. The time is always midnight UTC.                                                                                                                                                                            |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Type: String                                                                                                                                                                                                                                                |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Ancestor: Expiration, Transition                                                                                                                                                                                                                            |                                                                                                                                                   |
   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | Days                           | Indicates the number of days after object creation when the specified rule takes effect.                                                                                                                                                                    | Mandatory if the **Date** parameter is absent.                                                                                                    |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Type: Positive integer                                                                                                                                                                                                                                      |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Ancestor: Expiration, Transition                                                                                                                                                                                                                            |                                                                                                                                                   |
   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | StorageClass                   | Indicates the new storage class of the object.                                                                                                                                                                                                              | Mandatory if **Transition** or **NoncurrentVersionTransition** is present.                                                                        |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Type: **STANDARD_IA** or **GLACIER**                                                                                                                                                                                                                        |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Ancestor: **Transition, NoncurrentVersionTransition**                                                                                                                                                                                                       |                                                                                                                                                   |
   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | Transition                     | Indicates the element of the transition time and new storage class (applicable to the latest version of the object) in the lifecycle configuration.                                                                                                         | Mandatory if **NoncurrentVersionTransition**, **Expiration**, **AbortIncompleteMultipartUpload**, and **NoncurrentVersionExpiration** are absent. |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Type: XML                                                                                                                                                                                                                                                   |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Children: Date or Days, StorageClass                                                                                                                                                                                                                        |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Ancestor: Rule                                                                                                                                                                                                                                              |                                                                                                                                                   |
   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | Expiration                     | Indicates the container for the object expiration rule.                                                                                                                                                                                                     | Mandatory if **Transition**, **NoncurrentVersionTransition**, and **NoncurrentVersionExpiration** are absent.                                     |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Type: XML                                                                                                                                                                                                                                                   | Mandatory                                                                                                                                         |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Children: Date or Days                                                                                                                                                                                                                                      |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Ancestor: Rule                                                                                                                                                                                                                                              |                                                                                                                                                   |
   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | ID                             | Indicates the unique identifier of a rule. The value can contain a maximum of 255 characters.                                                                                                                                                               | Optional                                                                                                                                          |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Type: String                                                                                                                                                                                                                                                |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Ancestor: Rule                                                                                                                                                                                                                                              |                                                                                                                                                   |
   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | LifecycleConfiguration         | Indicates the container for lifecycle rules. You can add multiple rules. The total size of the rules cannot exceed 20 KB.                                                                                                                                   | Mandatory                                                                                                                                         |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Type: XML                                                                                                                                                                                                                                                   |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Children: Rule                                                                                                                                                                                                                                              |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Ancestor: None                                                                                                                                                                                                                                              |                                                                                                                                                   |
   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | NoncurrentDays                 | Indicates the number of days after object is noncurrent when the specified rule takes effect.                                                                                                                                                               | Mandatory if the **NoncurrentVersionExpiration** or **NoncurrentVersionTransition** parameter is present.                                         |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Type: Positive integer                                                                                                                                                                                                                                      |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Ancestor: NoncurrentVersionExpiration, NoncurrentVersionTransition                                                                                                                                                                                          |                                                                                                                                                   |
   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | NoncurrentVersionTransition    | Indicates the element of the transition time and new storage class (applicable to historical versions) in the lifecycle configuration.                                                                                                                      | Mandatory if **Transition**, **Expiration**, and **NoncurrentVersionExpiration** are absent.                                                      |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Type: XML                                                                                                                                                                                                                                                   |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Children: NoncurrentDays, StorageClass                                                                                                                                                                                                                      |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Ancestor: Rule                                                                                                                                                                                                                                              |                                                                                                                                                   |
   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | NoncurrentVersionExpiration    | Indicates the container for the noncurrent object expiration rule. You set this lifecycle configuration action on a bucket that has versioning enabled (or suspended) to request that OBS delete noncurrent object versions which meet the expiration rule. | Mandatory if **Transition**, **Expiration**, and **NoncurrentVersionTransition** are absent.                                                      |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Type: XML                                                                                                                                                                                                                                                   |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Children: NoncurrentDays                                                                                                                                                                                                                                    |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Ancestor: Rule                                                                                                                                                                                                                                              |                                                                                                                                                   |
   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | AbortIncompleteMultipartUpload | Container for specifying when the not merged parts (fragments) in an incomplete upload will be deleted.                                                                                                                                                     | Required if the **Transition**, **Expiration**, **NoncurrentVersionExpiration**, or **NoncurrentVersionTransition** element is absent.            |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Type: XML                                                                                                                                                                                                                                                   |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Children node: DaysAfterInitiation                                                                                                                                                                                                                          |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Ancestor node: Rule                                                                                                                                                                                                                                         |                                                                                                                                                   |
   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | DaysAfterInitiation            | Specifies the number of days since the initiation of an incomplete multipart upload that OBS will wait before deleting the not merged parts (fragments) of the upload.                                                                                      | Required if the **AbortIncompleteMultipartUpload** element is present.                                                                            |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Type: positive integer                                                                                                                                                                                                                                      |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Ancestor node: AbortIncompleteMultipartUpload                                                                                                                                                                                                               |                                                                                                                                                   |
   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | Prefix                         | Indicates the object key prefix identifying one or more objects to which the rule applies.                                                                                                                                                                  | Mandatory                                                                                                                                         |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Type: String                                                                                                                                                                                                                                                |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Ancestor: Rule                                                                                                                                                                                                                                              |                                                                                                                                                   |
   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | Rule                           | Indicates the container for lifecycle rules.                                                                                                                                                                                                                | Mandatory                                                                                                                                         |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Type: Container                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Ancestor: LifecycleConfiguration                                                                                                                                                                                                                            |                                                                                                                                                   |
   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | Status                         | Indicates whether the rule is enabled.                                                                                                                                                                                                                      | Mandatory                                                                                                                                         |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Type: String                                                                                                                                                                                                                                                |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Ancestor: Rule                                                                                                                                                                                                                                              |                                                                                                                                                   |
   |                                |                                                                                                                                                                                                                                                             |                                                                                                                                                   |
   |                                | Valid Values: Enabled, Disabled                                                                                                                                                                                                                             |                                                                                                                                                   |
   +--------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+

If the multi-version of a bucket is enabled or suspended, you can set **NoncurrentVersionExpiration** or **NoncurrentVersionTransition** to control the lifecycle of historical object versions. The lifecycle of a historical version depends on the time when the version becomes a historical one, that is, the version is overwritten by a new version (**NoncurrentDays**).

In deletion circumstances, if **NoncurrentDays** is 1, a version can only be deleted one day after it has become a historical version. For example, the V1 version of object A is created on the first day of a month, and its new version V2 is uploaded on the fifth day of the month. Then V1 becomes a historical version. One day later, that is, when the 0 o'clock of the seventh day comes, V1 expires. If an object version does not meet the deletion conditions, **NoncurrentDays** is 1, and **StorageClass** is **STANDARD_IA**, a version transitions to the Warm storage class one day after it has become a historical version. For example, the V1 version of object A is created on the first day of a month, and its new version V2 is uploaded on the fifth day of the month. Then V1 becomes a historical version. One day later, that is, when the 0 o'clock of the seventh day comes, V1 transitions to the Warm storage class. (Remarks: There is a delay of less than 48 hours for such a deletion or transition upon object expiration.)

The following lists the background processing for when the multi-version of a bucket is enabled or suspended and the object of the latest version meets expiration rules:

-  The multi-version of the bucket is enabled:

   -  If the object of the latest version is not **deletemarker**, a new **deletemarker** is generated for the object.
   -  If the object of the latest version is **deletemarker** and the object has this version only, the version will be deleted.
   -  If the object of the latest version is **deletemarker** and the object has other versions, all versions of the object remain unchanged.

-  The multi-version of the bucket is suspended:

   -  If the latest version is not null, **deletemarker** of a null version will be generated.
   -  If the latest version is null, the null version will be overwritten by **deletemarker** of a new null version.

If the bucket versioning is **Enabled** or **Suspended** and the latest version of the object meets the transition rule:

-  If the latest version is **deletemarker**, this version will not transition to another storage class.
-  If the latest version is **deletemarker** and the object meets the transition conditions, this version will transition to another storage class.

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
   Server: Server Name
   x-amz-request-id: request id
   x-amz-id-2: id
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   Date: date
   Content-Length: length

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request 1
----------------

.. code-block:: text

   PUT /?lifecycle HTTP/1.1
    User-Agent: curl/7.29.0
    Host: bucketname.obs.example.com
    Date: Thu, 05 Sep 2013 09:35:44 +0000
    Authorization: AWS B9A70C60A39C4D551A16:MOO0dUPmAAEXEe0/z+Q9LCx1Vzc=
    Content-MD5: Sa2ttwkV/+XRCwEHg4N8ow==
    Content-Length: 423
    Expect: 100-continue

   <LifecycleConfiguration>
   <Rule>
   <ID>delete-2-days</ID>
   <Prefix>test/</Prefix>
   <Status>Enabled</Status>
   <Expiration>
   <Days>365</Days>
   </Expiration>
   <NoncurrentVersionExpiration>
   <NoncurrentDays>365</NoncurrentDays>
   </NoncurrentVersionExpiration>
   <Transition>
   <Days>30</Days>
   <StorageClass>STANDARD_IA</StorageClass>
   </Transition>
   <Transition>
   <Days>60</Days>
   <StorageClass>GLACIER</StorageClass>
   </Transition>
   <NoncurrentVersionTransition>
   <NoncurrentDays>30</NoncurrentDays>
   <StorageClass>STANDARD_IA</StorageClass>
   </NoncurrentVersionTransition>
   <NoncurrentVersionTransition>
   <NoncurrentDays>60</NoncurrentDays>
   <StorageClass>GLACIER</StorageClass>
   </NoncurrentVersionTransition>
   <AbortIncompleteMultipartUpload>
   <DaysAfterInitiation>10</DaysAfterInitiation>
   </AbortIncompleteMultipartUpload>
   </Rule>
   </LifecycleConfiguration>

Sample Response 1
-----------------

.. code-block::

   HTTP/1.1 200 OK
    Date: Thu, 05 Sep 2013 09:35:44 GMT
    Server: OBS
    x-amz-request-id: 90E2BA0A420C00000140ED7A369007A2
    x-amz-id-2: t35S98JCFKUMswCPZCk+UTi/VOoiSenzi5J6wnoKCIMfXUsKYGgU5+daiWAYiY/8
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Length: 0

Sample Request 2
----------------

.. code-block:: text

   PUT /?lifecycle HTTP/1.1
   User-Agent: curl/7.29.0
   Host: bucketname.obs.example.comDate: Thu, 05 Sep 2015 09:35:44 +0000
   Authorization: AWS B9A70C60A39C4D551A16:MOO0dUPmAAEXEe0/z+Q9LCx1Vzc=
   Content-MD5: Sa2ttwkV/+XRCwEHg4N8ow==
   Content-Length: 423
   Expect: 100-continue
   <LifecycleConfiguration>
   <Rule>
   <ID>delete-2-days</ID>
   <Prefix>test/</Prefix>
   <Status>Enabled</Status>
   <Expiration>
   <Days>365</Days>
   </Expiration>
   <Transition>
   <Days>30</Days>
   <StorageClass>STANDARD_IA</StorageClass>
   </Transition>
   <Transition>
   <Days>60</Days>
   <StorageClass>GLACIER</StorageClass>
   </Transition>
   <NoncurrentVersionTransition>
   <NoncurrentDays>30</NoncurrentDays>
   <StorageClass>STANDARD_IA</StorageClass>
   </NoncurrentVersionTransition>
   <NoncurrentVersionTransition>
   <NoncurrentDays>60</NoncurrentDays>
   <StorageClass>GLACIER</StorageClass>
   </NoncurrentVersionTransition>
   <AbortIncompleteMultipartUpload>
   <DaysAfterInitiation>10</DaysAfterInitiation>
   </AbortIncompleteMultipartUpload>
   </Rule>
   </LifecycleConfiguration>

Sample Response 2
-----------------

.. code-block::

   HTTP/1.1 200 OK
   Date: Thu, 05 Sep 2015 09:35:44 GMT
   x-amz-request-id: 90E2BA0A420C00000140ED7A369007A2
   x-amz-id-2: t35S98JCFKUMswCPZCk+UTi/VOoiSenzi5J6wnoKCIMfXUsKYGgU5+daiWAYiY/8
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   Content-Length: 0

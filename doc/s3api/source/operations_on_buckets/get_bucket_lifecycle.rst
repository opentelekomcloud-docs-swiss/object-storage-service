:original_name: en-us_topic_0125560497.html

.. _en-us_topic_0125560497:

GET Bucket lifecycle
====================

You can use this operation to get the bucket lifecycle configuration.

Only users granted the **s3:GetLifecycleConfiguration** permission can view the bucket lifecycle configuration. By default, only the bucket owner can get the bucket lifecycle configuration. The bucket owner can allow other users to get the bucket lifecycle configuration by granting them the permission.

Request Syntax
--------------

.. code-block:: text

   GET /?lifecycle HTTP/1.1
   User-Agent: agent
    Host: bucketname.obs.example.com
   Accept: */*
   Date: date
    Authorization: authorization

Request Parameters
------------------

This request involves no parameters.

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

Request Elements
----------------

This request involves no elements.

Response Syntax
---------------

.. code-block::

   HTTP/1.1 200 OK
   Server: Server Name
   x-amz-request-id: 90E2BA0A420C00000140ED9939AF099E
   x-amz-id-2: UHQoAKndcsk628TszydX75G/Q2+I5MwYJ3IJYqzEkNInMkBMn96hunAVsoiMCHZh
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   Content-Type: application/xml
   Date: Thu, 05 Sep 2015 10:09:36 GMT
   Content-Length: 425

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <LifecycleConfiguration xmlns="http://obs.example.com/doc/2015-06-30/">
   <Rule>
   <ID>id</ID>
   <Prefix>prefix</Prefix>
   <Status>status</Status>
   <Expiration>
   <Date>date</Date>
   </Expiration>
   <NoncurrentVersionExpiration>
   <NoncurrentDays>365</NoncurrentDays>
   </NoncurrentVersionExpiration>
   <Transition>
   <Date>date</Date>
   <StorageClass>STANDARD_IA</StorageClass>
   </Transition>
   <Transition>
   <Date>date</Date>
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

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response contains elements to detail bucket lifecycle configuration. :ref:`Table 1 <en-us_topic_0125560497__table28619802>` describes the elements.

.. _en-us_topic_0125560497__table28619802:

.. table:: **Table 1** Response elements for lifecycle configuration

   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                                                                                                                                                                 |
   +===================================+=============================================================================================================================================================================================================================================================+
   | Date                              | Indicates when the specified rule takes effect.                                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | The date value must conform to ISO 8601 format. The time is always midnight UTC.                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Type: String                                                                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Ancestor: Expiration, Transition                                                                                                                                                                                                                            |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Days                              | Indicates the number of days after object creation when the specified rule takes effect.                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Type: Positive integer                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Ancestor: Expiration, Transition                                                                                                                                                                                                                            |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | StorageClass                      | Indicates the new storage class of the object.                                                                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Type: **STANDARD_IA** or **GLACIER**                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Ancestor: **Transition, NoncurrentVersionTransition**                                                                                                                                                                                                       |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Transition                        | Indicates the element of the transition time and new storage class (applicable to the latest version of the object) in the lifecycle configuration.                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Type: XML                                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Children: **Date** or **Days**                                                                                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Ancestor: **Rule**                                                                                                                                                                                                                                          |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Expiration                        | Indicates the container for the object expiration rule.                                                                                                                                                                                                     |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Type: XML                                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Children: Date or Days                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Ancestor: Rule                                                                                                                                                                                                                                              |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ID                                | Indicates the unique identifier of a rule. The value can contain a maximum of 255 characters.                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Type: String                                                                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Ancestor: Rule                                                                                                                                                                                                                                              |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | LifecycleConfiguration            | Indicates the container for lifecycle rules. You can add multiple rules. The total size of the rules cannot exceed 20 KB.                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Type: XML                                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Children: Rule                                                                                                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Ancestor: None                                                                                                                                                                                                                                              |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | NoncurrentDays                    | Indicates the number of days after object is noncurrent when the specified rule takes effect.                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Type: Positive integer                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Ancestor: NoncurrentVersionExpiration, NoncurrentVersionTransition                                                                                                                                                                                          |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | NoncurrentVersionTransition       | Indicates the element of the transition time and new storage class (applicable to historical versions) in the lifecycle configuration.                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Type: XML                                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Children: NoncurrentDays, StorageClass                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Ancestor: Rule                                                                                                                                                                                                                                              |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | NoncurrentVersionExpiration       | Indicates the container for the noncurrent object expiration rule. You set this lifecycle configuration action on a bucket that has versioning enabled (or suspended) to request that OBS delete noncurrent object versions which meet the expiration rule. |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Type: XML                                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Children: NoncurrentDays                                                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Ancestor: Rule                                                                                                                                                                                                                                              |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AbortIncompleteMultipartUpload    | Container for specifying when the not merged parts (fragments) in an incomplete upload will be deleted.                                                                                                                                                     |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Type: XML                                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Children node: DaysAfterInitiation                                                                                                                                                                                                                          |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Ancestor node: Rule                                                                                                                                                                                                                                         |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DaysAfterInitiation               | Specifies the number of days since the initiation of an incomplete multipart upload that OBS will wait before deleting the not merged parts (fragments) of the upload.                                                                                      |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Type: positive integer                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Ancestor node: AbortIncompleteMultipartUpload                                                                                                                                                                                                               |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Prefix                            | Indicates the object key prefix identifying one or more objects to which the rule applies.                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Type: String                                                                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Ancestor: Rule                                                                                                                                                                                                                                              |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Rule                              | Indicates the container for lifecycle rules.                                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Type: Container                                                                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Ancestor: LifecycleConfiguration                                                                                                                                                                                                                            |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Status                            | Indicates whether the rule is enabled.                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Type: String                                                                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Ancestor: Rule                                                                                                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                                                                             |
   |                                   | Valid Values: Enabled, Disabled                                                                                                                                                                                                                             |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

This response contains common errors. For details, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`. In addition, this response contains one special error, as described in :ref:`Table 2 <en-us_topic_0125560497__table56251627>`.

.. _en-us_topic_0125560497__table56251627:

.. table:: **Table 2** Special error

   +------------------------------+-------------------------------------------------------------------+------------------+
   | Error Code                   | Description                                                       | HTTP Status Code |
   +==============================+===================================================================+==================+
   | NoSuchLifecycleConfiguration | Indicates that the bucket lifecycle configuration does not exist. | 404 Not Found    |
   +------------------------------+-------------------------------------------------------------------+------------------+

Sample Request
--------------

.. code-block:: text

   GET /?lifecycle HTTP/1.1
   User-Agent: curl/7.29.0
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Thu, 05 Sep 2013 10:09:36 +0000
    Authorization: AWS B9A70C60A39C4D551A16:oNFuFZV8JLUqxsaFPI1Gs/HPRKg=

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
   Server: OBS
   x-amz-request-id: 90E2BA0A420C00000140ED9939AF099E
   x-amz-id-2: UHQoAKndcsk628TszydX75G/Q2+I5MwYJ3IJYqzEkNInMkBMn96hunAVsoiMCHZh
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   Content-Type: application/xml
   Date: Thu, 05 Sep 2015 10:09:36 GMT
   Content-Length: 425

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <LifecycleConfiguration xmlns="http://obs.example.com/doc/2015-06-30/">
   <Rule>
   <ID>delete-test/-1-day</ID>
   <Prefix>test/</Prefix>
   <Status>Enabled</Status>
   <Expiration>
   <Date>2015-07-12T00:00:00.000Z</Date>
   </Expiration>
   <NoncurrentVersionExpiration>
   <NoncurrentDays>365</NoncurrentDays>
   </NoncurrentVersionExpiration>
   <Transition>
   <Date>2015-07-10T00:00:00.000Z</Date>
   <StorageClass>STANDARD_IA</StorageClass>
   </Transition>
   <Transition>
   <Date>2015-07-11T00:00:00.000Z</Date>
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

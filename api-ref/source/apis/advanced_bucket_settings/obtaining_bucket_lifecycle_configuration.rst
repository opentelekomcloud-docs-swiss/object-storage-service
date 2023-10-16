:original_name: obs_04_0035.html

.. _obs_04_0035:

Obtaining Bucket Lifecycle Configuration
========================================

Functions
---------

This operation obtains the bucket lifecycle configuration.

To perform this operation, you must have the **GetLifecycleConfiguration** permission. By default, only the bucket owner can perform this operation. The bucket owner can grant the permission to other users by configuring the bucket policy or user policy.

Request Syntax
--------------

.. code-block:: text

   GET /?lifecycle HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Authorization: authorization

Request Parameters
------------------

This request contains no message parameters.

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Request Elements
----------------

This request involves no elements.

Response Syntax
---------------

::

   HTTP/1.1 status_code
   Date: date
   Content-Type: application/xml
   Date: date
   Content-Length: length

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <LifecycleConfiguration xmlns="http://obs.region.example.com/doc/2015-06-30/">
       <Rule>
           <ID>id</ID>
           <Prefix>prefix</Prefix>
           <Status>status</Status>
           <Expiration>
               <Date>date</Date>
           </Expiration>
           <NoncurrentVersionExpiration>
               <NoncurrentDays>days</NoncurrentDays>
           </NoncurrentVersionExpiration>
       </Rule>
   </LifecycleConfiguration>

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains elements to detail the configuration. :ref:`Table 1 <obs_04_0035__table11521331184255>` describes the elements.

.. _obs_04_0035__table11521331184255:

.. table:: **Table 1** Response elements for lifecycle configuration

   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
   +===================================+===================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
   | Date                              | Specifies that OBS executes lifecycle rules for objects before the specified date. The date must be compliant with the ISO8601 format, and the time must be compliant with the UTC format of 00:00:00. For example, **2018-01-01T00:00:00.000Z** indicates that objects whose last modification time is earlier than **2018-01-01T00:00:00.000Z** are deleted. Objects whose last modification time is equal to or later than the specified time are not deleted. |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Type: string                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Ancestor node: Expiration                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Days                              | Specifies the number of days (since the latest update to the latest object version) after which the lifecycle rule is executed.                                                                                                                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Type: integer                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Ancestor node: Expiration                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Expiration                        | Container for the object expiration rule.                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Type: XML                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Children node: Date or Days                                                                                                                                                                                                                                                                                                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Ancestor node: Rule                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ID                                | Unique identifier of a rule. The value can contain a maximum of 255 characters.                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Type: string                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Ancestor node: Rule                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | LifecycleConfiguration            | Container for lifecycle rules. You can add multiple rules. The total size of the rules cannot exceed 20 KB.                                                                                                                                                                                                                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Type: XML                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Children node: Rule                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Ancestor node: none                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | NoncurrentDays                    | Number of days when the specified rule takes effect after the object becomes a historical version.                                                                                                                                                                                                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Type: integer                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Ancestor node: NoncurrentVersionExpiration                                                                                                                                                                                                                                                                                                                                                                                                                        |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | NoncurrentVersionExpiration       | Container for the expiration time of objects' historical versions. If versioning is enabled or suspended for a bucket, you can set **NoncurrentVersionExpiration** to delete objects whose life cycles have expired.                                                                                                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Type: XML                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Children node: NoncurrentDays                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Ancestor node: Rule                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Prefix                            | Object name prefix identifying one or more objects to which the rule applies.                                                                                                                                                                                                                                                                                                                                                                                     |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Type: string                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Ancestor node: Rule                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Rule                              | Container for a specific lifecycle rule.                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Type: container                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Ancestor node: LifecycleConfiguration                                                                                                                                                                                                                                                                                                                                                                                                                             |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Status                            | Indicates whether the rule is enabled.                                                                                                                                                                                                                                                                                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Type: string                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Ancestor node: Rule                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   | Value options: **Enabled**, **Disabled**                                                                                                                                                                                                                                                                                                                                                                                                                          |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

:ref:`Table 2 <obs_04_0035__table1335025184517>` describes possible special errors in the request.

.. _obs_04_0035__table1335025184517:

.. table:: **Table 2** Special error

   +------------------------------+----------------------------------------------------+------------------+
   | Error Code                   | Description                                        | HTTP Status Code |
   +==============================+====================================================+==================+
   | NoSuchLifecycleConfiguration | The bucket lifecycle configuration does not exist. | 404 Not Found    |
   +------------------------------+----------------------------------------------------+------------------+

For other errors, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   GET /?lifecycle HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 03:06:56 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:/Nof9FCNANfzIXDS0NDp1IfDu8I=

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: BF260000016436BA5684FF5A10370EDB
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSEMKZSIeboCA1eAukgYOOAd7oX3ZONn
   Content-Type: application/xml
   Date: WED, 01 Jul 2015 03:06:56 GMT
   Content-Length: 919

   <?xml version="1.0" encoding="utf-8"?>
   <LifecycleConfiguration>
     <Rule>
       <ID>delete-2-days</ID>
       <Status>Enabled</Status>
       <Expiration>
         <Days>2</Days>
       </Expiration>
       <NoncurrentVersionExpiration>
         <NoncurrentDays>5</NoncurrentDays>
       </NoncurrentVersionExpiration>
     </Rule>
   </LifecycleConfiguration>

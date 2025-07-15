:original_name: en-us_topic_0000001198597564.html

.. _en-us_topic_0000001198597564:

GET Bucket Inventory
====================

OBS uses the GET method to obtain a specific inventory of a bucket.

To perform this operation, you must have the **GetBucketInventoryConfiguration** permission. By default, the bucket owner has this permission and can assign this permission to other users.

Request Syntax
--------------

.. code-block:: text

   GET /?inventory&id=configuration-id HTTP/1.1
   User-Agent: curl/7.29.0
   Host: bucketname.obs.region.example.com
   Accept: */*
   Date: date
   Authorization: authorization string

Request Parameters
------------------

.. table:: **Table 1** Request parameters

   +-----------------------+---------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                     | Mandatory             |
   +=======================+=================================================================================+=======================+
   | id                    | ID of the inventory configuration that you want to obtain.                      | Yes                   |
   |                       |                                                                                 |                       |
   |                       | Type: string                                                                    |                       |
   |                       |                                                                                 |                       |
   |                       | Specifications: A maximum of 64 characters                                      |                       |
   |                       |                                                                                 |                       |
   |                       | There is no default value.                                                      |                       |
   |                       |                                                                                 |                       |
   |                       | Valid characters: letters, digits, hyphens (-), periods (.) and underscores (_) |                       |
   +-----------------------+---------------------------------------------------------------------------------+-----------------------+

Request Headers
---------------

This request uses common headers. For details about common request headers, see the section :ref:`Common Request Headers <en-us_topic_0125560462>`.

Request Elements
----------------

This request involves no elements.

Response Syntax
---------------

::

   HTTP/1.1 status_code
   Server: OBS
   x-amz-request-id: request id
   x-amz-id-2: id
   Content-Type: application/xml
   Date: date
   Content-Length: length

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <InventoryConfiguration  xmlns="http://obs.region.example.com/doc/2015-06-30/">
     <Id>configuration-id</Id>
     <IsEnabled>true</IsEnabled>
     <Destination>
       <Format>CSV</Format>
       <Bucket>destbucket</Bucket>
       <Prefix>prefix</Prefix>
     </Destination>
     <Schedule>
       <Frequency>Daily</Frequency>
     </Schedule>
     <IncludedObjectVersions>Current</IncludedObjectVersions>
     <OptionalFields>
       <Field>Size</Field>
       <Field>LastModifiedDate</Field>
       <Field>ETag</Field>
       <Field>StorageClass</Field>
       <Field>IsMultipartUploaded</Field>
       <Field>ReplicationStatus</Field>
     </OptionalFields>
   </InventoryConfiguration>

Response Headers
----------------

This response uses common headers. For details about common response headers, see the section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

:ref:`Table 2 <en-us_topic_0000001198597564__table1181123018399>` lists elements contained in the response body.

.. _en-us_topic_0000001198597564__table1181123018399:

.. table:: **Table 2** Elements in a response body to the request for bucket inventory configurations

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                                                                                                                                            |
   +===================================+========================================================================================================================================================================================================================================+
   | InventoryConfiguration            | Inventory configuration.                                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Type: container                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Ancestor: none                                                                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Children: Id, IsEnabled, Filter, Destination, Schedule, IncludedObjectVersions, and OptionalFields                                                                                                                                     |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Id                                | ID of an inventory configuration, which must be consistent with the inventory configuration ID specified in the request.                                                                                                               |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Type: string                                                                                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Specifications: A maximum of 64 characters                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | There is no default value.                                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Valid characters: letters, digits, hyphens (-), periods (.) and underscores (_)                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Ancestor: InventoryConfiguration                                                                                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | IsEnabled                         | Indicates whether the rule is enabled. If this parameter is set to **true**, the inventory is generated. If not, the inventory will not be generated.                                                                                  |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Type: boolean                                                                                                                                                                                                                          |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Valid values: **true** or **false**                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Ancestor: InventoryConfiguration                                                                                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Filter                            | Inventory filter configuration. The inventory contains only objects that meet the filter criteria (filtering by object name prefix). If no filter criteria is configured, all objects are included.                                    |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Type: container                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Ancestor: InventoryConfiguration                                                                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Children: Prefix                                                                                                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Prefix                            | Filtering by name prefix. Only objects with the specified name prefix are included in the inventory.                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Type: string                                                                                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Ancestor: Filter                                                                                                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Schedule                          | Time scheduled for generation of inventories.                                                                                                                                                                                          |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Type: container                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Ancestor: InventoryConfiguration                                                                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Children: Frequency                                                                                                                                                                                                                    |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Frequency                         | Intervals when inventories are generated. You can set this parameter to **Daily** or **Weekly**. An inventory is generated within one hour after it is configured for the first time. Then it is generated at the specified intervals. |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Type: string                                                                                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Ancestor: Schedule                                                                                                                                                                                                                     |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Valid values: **Daily** or **Weekly**                                                                                                                                                                                                  |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Destination                       | Destination bucket of an inventory.                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Type: container                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Ancestor: InventoryConfiguration                                                                                                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Format                            | Inventory format. Only the CSV format is supported.                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Type: string                                                                                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Ancestor: Destination                                                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Valid values: **CSV**                                                                                                                                                                                                                  |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Bucket                            | Name of the bucket for saving inventories.                                                                                                                                                                                             |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Type: string                                                                                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Ancestor: Destination                                                                                                                                                                                                                  |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Prefix                            | The name prefix of inventory files. If no prefix is configured, the names of inventory files will start with the **BucketInventory** by default.                                                                                       |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Type: string                                                                                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Ancestor: Destination                                                                                                                                                                                                                  |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | IncludedObjectVersions            | Indicates whether versions of objects are included in an inventory.                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | -  If this parameter is set to **All**, all the versions of objects are included in the inventory, and versioning related fields are added to the inventory, including: **VersionId**, **IsLatest**, and **DeleteMarker**.             |
   |                                   | -  If this parameter is set to **Current**, the inventory contains only the current objects versions at the time when the inventory is generated. No versioning fields are displayed in the inventory.                                 |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Type: string                                                                                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Ancestor: InventoryConfiguration                                                                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Valid values: **All** or **Current**                                                                                                                                                                                                   |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | OptionalFields                    | Extra metadata fields that can be added to an inventory. If this parameter is configured, fields specified in this parameter are contained in the inventory.                                                                           |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Type: container                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Ancestor: InventoryConfiguration                                                                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Children: Field                                                                                                                                                                                                                        |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Field                             | Optional fields. The **OptionalFields** can contain multiple field elements.                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Type: string                                                                                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Ancestor: OptionalFields                                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                        |
   |                                   | Valid values: **Size**, **LastModifiedDate**, **StorageClass**, **ETag**, **IsMultipartUploaded**, **ReplicationStatus**.                                                                                                              |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

In addition common error codes, this API also returns other error codes. The following table lists common errors and possible causes. For details, see :ref:`Table 3 <en-us_topic_0000001198597564__table1488314173514>`.

.. _en-us_topic_0000001198597564__table1488314173514:

.. table:: **Table 3** Error codes related to obtaining inventory configurations

   +------------------------------+-------------------------------------------------------------+------------------+
   | Error Code                   | Description                                                 | HTTP Status Code |
   +==============================+=============================================================+==================+
   | NoSuchInventoryConfiguration | No inventory configuration found matching the specified ID. | 404 Not Found    |
   +------------------------------+-------------------------------------------------------------+------------------+

Sample Request
--------------

.. code-block:: text

   GET /?inventory&id=id1 HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: Tue, 08 Jan 2019 09:32:24 +0000
   Authorization: AWS UDSIAMSTUBTEST000001:ySWncC9M08jNsyXdJLSMJkpi7XM=

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-amz-request-id: 000001682CB4C2EE6808A0D8DF9F3D00
   x-amz-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSBjn5O7Jv9CqvUMO0BenehRdil1n8rR
   Content-Type: application/xml
   Date: Tue, 08 Jan 2019 09:04:30 GMT
   Content-Length: 626

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <InventoryConfiguration  xmlns="http://obs.region.example.com/doc/2015-06-30/">
     <Id>id1</Id>
     <IsEnabled>true</IsEnabled>
     <Destination>
       <Format>CSV</Format>
       <Bucket>bucket</Bucket>
       <Prefix>prefix</Prefix>
     </Destination>
     <Schedule>
       <Frequency>Daily</Frequency>
     </Schedule>
     <IncludedObjectVersions>Current</IncludedObjectVersions>
     <OptionalFields>
       <Field>Size</Field>
       <Field>LastModifiedDate</Field>
       <Field>ETag</Field>
       <Field>StorageClass</Field>
       <Field>IsMultipartUploaded</Field>
       <Field>ReplicationStatus</Field>
     </OptionalFields>
   </InventoryConfiguration>

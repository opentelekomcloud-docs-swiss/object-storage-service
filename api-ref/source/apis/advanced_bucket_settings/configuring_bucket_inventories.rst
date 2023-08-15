:original_name: obs_04_0055.html

.. _obs_04_0055:

Configuring Bucket Inventories
==============================

Functions
---------

OBS uses the PUT method to configure bucket inventories. Each bucket can have a maximum of 10 inventories.

To perform this operation, ensure that you have the **PutBucketInventoryConfiguration** permission. By default, the bucket owner has this permission and can assign this permission to other users.

Request Syntax
--------------

.. code-block:: text

   PUT /?inventory&id=configuration-id  HTTP/1.1
   User-Agent: curl/7.29.0
   Host: bucketname.obs.region.example.com
   Accept: */*
   Date: date
   Authorization: authorization string
   Content-Length: length
   Expect: 100-continue

   <InventoryConfiguration>
      <Id>configuration-id</Id>
      <IsEnabled>true</IsEnabled>
      <Filter>
            <Prefix>inventoryTestPrefix</Prefix>
      </Filter>
      <Destination>
            <Format>CSV</Format>
            <Bucket>destbucket</Bucket>
            <Prefix>dest-prefix</Prefix>
      </Destination>
      <Schedule>
             <Frequency>Daily</Frequency>
      </Schedule>
      <IncludedObjectVersions>All</IncludedObjectVersions>
      <OptionalFields>
             <Field>Size</Field>
             <Field>LastModifiedDate</Field>
             <Field>ETag</Field>
             <Field>StorageClass</Field>
             <Field>IsMultipartUploaded</Field>
             <Field>ReplicationStatus</Field>
             <Field>EncryptionStatus</Field>
      </OptionalFields>
   </InventoryConfiguration>

Request Parameters
------------------

.. table:: **Table 1** Request parameters

   +-----------------------+----------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                                          | Mandatory             |
   +=======================+======================================================================================================================+=======================+
   | id                    | ID of the inventory configuration, which must be consistent with the inventory configuration ID in the message body. | Yes                   |
   |                       |                                                                                                                      |                       |
   |                       | Type: string                                                                                                         |                       |
   |                       |                                                                                                                      |                       |
   |                       | Specifications: A maximum of 64 characters                                                                           |                       |
   |                       |                                                                                                                      |                       |
   |                       | There is no default value.                                                                                           |                       |
   |                       |                                                                                                                      |                       |
   |                       | Valid characters: letters, digits, hyphens (-), periods (.) and underscores (_)                                      |                       |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------+-----------------------+

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Request Elements
----------------

In this request, you must configure the bucket inventory in the request body. Upload the inventory configuration information in an XML file. :ref:`Table 2 <obs_04_0055__table1181123018399>` lists the configuration elements.

.. _obs_04_0055__table1181123018399:

.. table:: **Table 2** Bucket inventory configuration elements

   +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Element                | Description                                                                                                                                                                                                                            | Mandatory             |
   +========================+========================================================================================================================================================================================================================================+=======================+
   | InventoryConfiguration | Inventory configuration.                                                                                                                                                                                                               | Yes                   |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Type: container                                                                                                                                                                                                                        |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Ancestor: none                                                                                                                                                                                                                         |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Children: Id, IsEnabled, Filter, Destination, Schedule, IncludedObjectVersions, and OptionalFields                                                                                                                                     |                       |
   +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Id                     | ID of an inventory configuration, which must be consistent with the inventory configuration ID specified in the request.                                                                                                               | Yes                   |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Type: string                                                                                                                                                                                                                           |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Specifications: A maximum of 64 characters                                                                                                                                                                                             |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | There is no default value.                                                                                                                                                                                                             |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Valid characters: letters, digits, hyphens (-), periods (.) and underscores (_)                                                                                                                                                        |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Ancestor: InventoryConfiguration                                                                                                                                                                                                       |                       |
   +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | IsEnabled              | Indicates whether the rule is enabled. If this parameter is set to **true**, the inventory is generated. If not, the inventory will not be generated.                                                                                  | Yes                   |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Type: boolean                                                                                                                                                                                                                          |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Valid values: **true** or **false**                                                                                                                                                                                                    |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Ancestor: InventoryConfiguration                                                                                                                                                                                                       |                       |
   +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Filter                 | Inventory filter configuration. The inventory contains only objects that meet the filter criteria (filtering by object name prefix). If no filter criteria is configured, all objects are included.                                    | No                    |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Type: container                                                                                                                                                                                                                        |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Ancestor: InventoryConfiguration                                                                                                                                                                                                       |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Children: Prefix                                                                                                                                                                                                                       |                       |
   +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Prefix                 | Filtering by name prefix. Only objects with the specified name prefix are included in the inventory.                                                                                                                                   | No                    |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Type: string                                                                                                                                                                                                                           |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Ancestor: Filter                                                                                                                                                                                                                       |                       |
   +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Schedule               | Time scheduled for generation of inventories.                                                                                                                                                                                          | Yes                   |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Type: container                                                                                                                                                                                                                        |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Ancestor: InventoryConfiguration                                                                                                                                                                                                       |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Children: Frequency                                                                                                                                                                                                                    |                       |
   +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Frequency              | Intervals when inventories are generated. You can set this parameter to **Daily** or **Weekly**. An inventory is generated within one hour after it is configured for the first time. Then it is generated at the specified intervals. | Yes                   |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Type: string                                                                                                                                                                                                                           |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Ancestor: Schedule                                                                                                                                                                                                                     |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Valid values: **Daily** or **Weekly**                                                                                                                                                                                                  |                       |
   +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Destination            | Destination bucket of an inventory.                                                                                                                                                                                                    | Yes                   |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Type: container                                                                                                                                                                                                                        |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Ancestor: InventoryConfiguration                                                                                                                                                                                                       |                       |
   +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Format                 | Inventory format. Only the CSV format is supported.                                                                                                                                                                                    | Yes                   |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Type: string                                                                                                                                                                                                                           |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Ancestor: Destination                                                                                                                                                                                                                  |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Valid values: **CSV**                                                                                                                                                                                                                  |                       |
   +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Bucket                 | Name of the bucket for saving inventories.                                                                                                                                                                                             | Yes                   |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Type: string                                                                                                                                                                                                                           |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Ancestor: Destination                                                                                                                                                                                                                  |                       |
   +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Prefix                 | The name prefix of inventory files. If no prefix is configured, the names of inventory files will start with the **BucketInventory** by default.                                                                                       | No                    |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Type: string                                                                                                                                                                                                                           |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Ancestor: Destination                                                                                                                                                                                                                  |                       |
   +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | IncludedObjectVersions | Indicates whether versions of objects are included in an inventory.                                                                                                                                                                    | Yes                   |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | -  If this parameter is set to **All**, all the versions of objects are included in the inventory, and versioning related fields are added to the inventory, including: **VersionId**, **IsLatest**, and **DeleteMarker**.             |                       |
   |                        | -  If this parameter is set to **Current**, the inventory contains only the current objects versions at the time when the inventory is generated. No versioning fields are displayed in the inventory.                                 |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Type: string                                                                                                                                                                                                                           |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Ancestor: InventoryConfiguration                                                                                                                                                                                                       |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Valid values: **All** or **Current**                                                                                                                                                                                                   |                       |
   +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | OptionalFields         | Extra metadata fields that can be added to an inventory. If this parameter is configured, fields specified in this parameter are contained in the inventory.                                                                           | No                    |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Type: container                                                                                                                                                                                                                        |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Ancestor: InventoryConfiguration                                                                                                                                                                                                       |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Children: Field                                                                                                                                                                                                                        |                       |
   +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Field                  | Optional fields. The **OptionalFields** can contain multiple field elements.                                                                                                                                                           | No                    |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Type: string                                                                                                                                                                                                                           |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Ancestor: OptionalFields                                                                                                                                                                                                               |                       |
   |                        |                                                                                                                                                                                                                                        |                       |
   |                        | Valid values: **Size**, **LastModifiedDate**, **StorageClass**, **ETag**, **IsMultipartUploaded**, **ReplicationStatus**, and **EncryptionStatus**.                                                                                    |                       |
   +------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

Response Syntax
---------------

::

   HTTP/1.1 status_code
   x-obs-request-id: request id
   x-obs-id-2: id
   Date: date
   Content-Length: length

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

In addition common error codes, this API also returns other error codes. The following lists some common errors and possible causes of this API. For details, see :ref:`Table 3 <obs_04_0055__table12876123320500>`.

.. _obs_04_0055__table12876123320500:

.. table:: **Table 3** Inventory configuration error codes

   +----------------------------------+------------------------------------------------------------------------------------------+------------------+
   | Error Code                       | Description                                                                              | HTTP Status Code |
   +==================================+==========================================================================================+==================+
   | MalformedXML                     | Incorrect XML format of the inventory.                                                   | 400 Bad Request  |
   +----------------------------------+------------------------------------------------------------------------------------------+------------------+
   | InvalidArgument                  | Invalid parameter.                                                                       | 400 Bad Request  |
   +----------------------------------+------------------------------------------------------------------------------------------+------------------+
   | InventoryCountOverLimit          | The number of inventories reached the upper limit.                                       | 400 Bad Request  |
   +----------------------------------+------------------------------------------------------------------------------------------+------------------+
   | PrefixExistInclusionRelationship | The prefix configured for this inventory overlaps with prefixes of existing inventories. | 400 Bad Request  |
   +----------------------------------+------------------------------------------------------------------------------------------+------------------+

Sample Request
--------------

.. code-block:: text

   PUT /?inventory&id=test_id HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: Tue, 08 Jan 2019 08:17:10 +0000
   Authorization: OBS UDSIAMSTUBTEST000001:/e2fqSfzLDb+0M36D4Op/s5KKr0=
   Content-Length: 600
   Expect: 100-continue

   <InventoryConfiguration>
      <Id>test_id</Id>
      <IsEnabled>true</IsEnabled>
      <Filter>
            <Prefix>inventoryTestPrefix</Prefix>
      </Filter>
      <Destination>
            <Format>CSV</Format>
            <Bucket>destbucket</Bucket>
            <Prefix>dest-prefix</Prefix>
      </Destination>
      <Schedule>
             <Frequency>Daily</Frequency>
      </Schedule>
      <IncludedObjectVersions>All</IncludedObjectVersions>
      <OptionalFields>
             <Field>Size</Field>
             <Field>LastModifiedDate</Field>
             <Field>ETag</Field>
             <Field>StorageClass</Field>
             <Field>IsMultipartUploaded</Field>
             <Field>ReplicationStatus</Field>
             <Field>EncryptionStatus</Field>
      </OptionalFields>
   </InventoryConfiguration>

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: 000001682C8545B0680893425D60AB83
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSIGTuRtBfo7lpHSt0ZknhdDHmllwd/p
   Date: Tue, 08 Jan 2019 08:12:38 GMT
   Content-Length: 0

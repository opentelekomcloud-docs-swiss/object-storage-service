:original_name: obs_04_0057.html

.. _obs_04_0057:

Listing All Inventories of a Bucket
===================================

Functions
---------

OBS uses the GET method without inventory IDs to obtain all inventories of a specified bucket. Obtained inventories are returned together on only one page.

To perform this operation, you must have the **GetBucketInventoryConfiguration** permission. By default, only the bucket owner can delete the tags of a bucket. The bucket owner can allow other users to perform this operation by setting a bucket policy or granting them the permission.

Request Syntax
--------------

.. code-block:: text

   GET /?inventory HTTP/1.1
   User-Agent: curl/7.29.0
   Host: bucketname.obs.region.example.com
   Accept: */*
   Date: date
   Authorization: authorization string

Request Parameters
------------------

This request message does not contain the request parameters.

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
   Server: OBS
   x-obs-request-id: request id
   x-obs-id-2: id
   Content-Type: application/xml
   Date: date
   Content-Length: length

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <ListInventoryConfiguration  xmlns="http://obs.region.example.com/doc/2015-06-30/">
    <InventoryConfiguration>
     <Id>id</Id>
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
        <Field>EncryptionStatus</Field>
      </OptionalFields>
    </InventoryConfiguration>
   </ListInventoryConfiguration>

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

:ref:`Table 1 <obs_04_0057__table1181123018399>` lists elements contained in the response body.

.. _obs_04_0057__table1181123018399:

.. table:: **Table 1** Bucket inventory configuration elements

   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                                         |
   +===================================+=====================================================================================================================================+
   | ListInventoryConfiguration        | List of bucket inventories.                                                                                                         |
   |                                   |                                                                                                                                     |
   |                                   | Type: container                                                                                                                     |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
   | InventoryConfiguration            | Bucket inventory configuration. For details about the configuration elements, see :ref:`Table 2 <obs_04_0056__table1181123018399>`. |
   |                                   |                                                                                                                                     |
   |                                   | Type: container                                                                                                                     |
   |                                   |                                                                                                                                     |
   |                                   | Parent: ListInventoryConfiguration                                                                                                  |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   GET /?inventory HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: Tue, 08 Jan 2019 09:32:24 +0000
   Authorization: OBS UDSIAMSTUBTEST000001:ySWncC9M08jNsyXdJLSMJkpi7XM=

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: 000001682CB4C2EE6808A0D8DF9F3D00
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSBjn5O7Jv9CqvUMO0BenehRdil1n8rR
   Content-Type: application/xml
   Date: Tue, 08 Jan 2019 09:04:30 GMT
   Content-Length: 626

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <ListInventoryConfiguration  xmlns="http://obs.region.example.com/doc/2015-06-30/">
    <InventoryConfiguration>
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
        <Field>EncryptionStatus</Field>
      </OptionalFields>
    </InventoryConfiguration>
   </ListInventoryConfiguration>

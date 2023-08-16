:original_name: en-us_topic_0000001243597437.html

.. _en-us_topic_0000001243597437:

DELETE Bucket Inventory
=======================

OBS uses the DELETE method to delete inventories (identified by inventory IDs) of a specified bucket.

To perform this operation, you must have the **DeleteBucketInventoryConfiguration** permission. By default, only the bucket owner can delete the tags of a bucket. The bucket owner can allow other users to perform this operation by setting a bucket policy or granting them the permission.

Request Syntax
--------------

.. code-block:: text

   DELETE /?inventory&id=configuration-id HTTP/1.1
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
   | Parameter             | Description                                                                     | Mandatory             |
   |                       |                                                                                 |                       |
   | id                    | ID of the inventory to be deleted.                                              | Yes                   |
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
   Date: date

Response Headers
----------------

This response uses common headers. For details about common response headers, see the section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   DELETE /test?inventory&id=id1 HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: Tue, 08 Jan 2019 13:18:35 +0000
   Authorization: AWS UDSIAMSTUBTEST000001:UT9F2YUgaFu9uFGMmxFj2CBgQHs=

Sample Response
---------------

::

   HTTP/1.1 204 No Content
   Server: OBS
   x-amz-request-id: 000001682D993B666808E265A3F6361D
   x-amz-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSyB46jGSQsu06m1nyIeKxTuJ+H27ooC
   Date: Tue, 08 Jan 2019 13:14:03 GMT

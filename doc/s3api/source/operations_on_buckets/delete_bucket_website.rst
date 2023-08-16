:original_name: en-us_topic_0125560295.html

.. _en-us_topic_0125560295:

DELETE Bucket website
=====================

You can use this operation to delete the website configuration of a bucket.

Only users granted the **s3:DeleteBucketWebsite** permission can delete the bucket website configuration. By default, only the bucket owner can delete the bucket website configuration. The bucket owner can allow other users to delete the bucket website configuration by granting them the permission.

Request Syntax
--------------

.. code-block::

    DELETE /?website HTTP/1.1
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

   HTTP/1.1 status_code
    Server: Server Name
    x-amz-request-id: request id
    x-amz-id-2: id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Date: date

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   DELETE /?website HTTP/1.1
    User-Agent: curl/7.29.0
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Sat, 04 Jan 2014 06:55:26 +0000
    Authorization: AWS C6630CD15B645CB8A3BA:iWz49B3sO2HTFlcsKdEsSULl5GI=

Sample Response
---------------

.. code-block::

   HTTP/1.1 204 No Content
    Server: OBS
    x-amz-request-id: DCD2FC9CAB78000001435C08F1018EDD
    x-amz-id-2: QeEqZzxKPinUt9LmE9sFGcR+5xCpm2HoqFCqFFuFAB9Y84NcX6/MjhZqpN0+cE2P
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Date: Sat, 04 Jan 2014 06:55:26 GMT

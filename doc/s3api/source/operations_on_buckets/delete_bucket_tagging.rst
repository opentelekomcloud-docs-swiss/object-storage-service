:original_name: en-us_topic_0125560426.html

.. _en-us_topic_0125560426:

DELETE Bucket tagging
=====================

This implementation of the **DELETE** operation uses the **tagging** subresource to remove a tag set from the specified bucket.

Only users granted the **s3:PutBucketTagging** permission can perform this operation. By default, the permission is granted to the bucket owner only. However, it can be granted to other users by configuring the bucket policy.

Request Syntax
--------------

.. code-block:: text

   DELETE /?tagging HTTP/1.1
   User-Agent: agent
   Host: bucketname.obs.example.com
   Accept: */*
   Date: date
   Authorization: authorization string

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

   HTTP/1.1 204 No Content
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

   DELETE /?tagging HTTP/1.1
   User-Agent: curl/7.19.7 (x86_64-suse-linux-gnu) libcurl/7.19.7 OpenSSL/0.9.8j zlib/1.2.7 libidn/1.10
   Host: bucketname.obs.example.com
   Accept: */*
   Date: Tue, 09 May 2017 03:07:13 +0000
   Authorization: authorization string

Sample Response
---------------

.. code-block::

   HTTP/1.1 204 No Content
   Server: OBS
   x-amz-request-id: request id
   x-amz-id-2: id
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   Date: Tue, 09 May 2017 03:06:29 GMT

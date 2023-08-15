:original_name: en-us_topic_0125560427.html

.. _en-us_topic_0125560427:

DELETE Bucket policy
====================

You can use this operation to delete the policy of a specified bucket.

Only the bucket owner can delete the bucket policy.

OBS returns **204 No Content** whether a requested bucket policy exists or not.

Request Syntax
--------------

.. code-block:: text

   DELETE /?policy HTTP/1.1
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
    Content-Type: type

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   DELETE /?policy HTTP/1.1
   Host: bucketname.obs.example.com
   Accept: */*
   Date: Fri, 06 Sep 2013 07:06:42 GMT
   Authorization: signature

Sample Response
---------------

.. code-block::

   HTTP/1.1 204 No Content
   Server: OBS
   x-amz-request-id: 7B6DFC9BC71DD58B061285551605709
   x-amz-id-2: N0I2REZDOUJDNzFERDU4QjA2MTI4NTU1MTYwNTcwOUFBQUFBQUFBYmJiYmJiYmJD
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   Content-Type: text/xml
   Date: Mon, 27 Sep 2010 01:40:03 GMT

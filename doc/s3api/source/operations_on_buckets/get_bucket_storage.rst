:original_name: en-us_topic_0125560293.html

.. _en-us_topic_0125560293:

GET Bucket storage
==================

Using this operation, the bucket owner can obtain the bucket's storage information such as the bucket size and number of objects in the bucket. The bucket size is a nonnegative integer, expressed in bytes.

Request Syntax
--------------

.. code-block:: text

   GET /?storageinfo HTTP/1.1
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
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: id
    Content-Type: type
    Date: date
    Content-Length: length
    <Response Body>

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

   GET /?storageinfo HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept-Encoding: gzip,deflate
    Date: Sat, 20 Oct 2012 06:23:16 +0000
    Authorization: AWS 08350B985315591007AD:O4jTB/FzS3gXDouwRZgz1wiE2PE=

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: 001B21D48A580000013A7CD702AB0011
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-amz-id-2: 8NgBZD4YTt+Gi11OlhtdGE/zB1d/q6btnc+L3E5Iq0VU80pf+GtXUfZ9lVmrhU6J
    Content-Type: application/xml
    Date: Sat, 20 Oct 2012 06:23:16 GMT
    Content-Length: 209

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <GetBucketStorageInfoResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <Size>14960</Size>
    <ObjectNumber>11</ObjectNumber>
    </GetBucketStorageInfoResult>

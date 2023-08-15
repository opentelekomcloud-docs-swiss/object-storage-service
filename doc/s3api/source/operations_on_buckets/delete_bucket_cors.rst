:original_name: en-us_topic_0125560432.html

.. _en-us_topic_0125560432:

DELETE Bucket CORS
==================

You can use this operation to delete the CORS configuration of a bucket.

After the CORS configuration is deleted, the bucket and objects in it cannot be accessed by requests from other websites.

Only users granted the **s3:PutBucketCORS** permission can perform this operation. By default, only the bucket owner can perform this operation. The bucket owner can allow other users to perform this operation by granting them the permission.

Request Syntax
--------------

.. code-block:: text

   DELETE /?cors HTTP/1.1
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

   DELETE /?cors HTTP/1.1
    User-Agent: curl/7.19.0 (x86_64-suse-linux-gnu) libcurl/7.19.0 OpenSSL/0.9.8{ zlib/1.2.3 libidn/1.10
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Tue, 28 Apr 2015 09:34:51 +0000
    Authorization: AWS D13E0C94E722DD69423C:YiZ7gMEMnxjYM32AjsCpoR4FpoI=

Sample Response
---------------

.. code-block::

   HTTP/1.1 204 No Content
    Server: OBS
    x-amz-request-id: 400535B2BF32AD9B6B21873AF4D5A57D
    x-amz-id-2: ihd0YbWuLj8XsU7IZKQFqK9KPoPean7wCQ2QYLqv9lkOCNr40+67DneNvK3Nfjt6
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Date: Tue, 28 Apr 2015 09:34:51 GMT

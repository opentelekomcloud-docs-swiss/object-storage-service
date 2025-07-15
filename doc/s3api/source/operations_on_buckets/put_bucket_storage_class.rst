:original_name: en-us_topic_0125560403.html

.. _en-us_topic_0125560403:

PUT Bucket storage class
========================

You can use this operation to create a default storage class for a bucket or change the default storage class of a bucket.

Only users granted the **s3:PutBucketStoragePolicy** permission can perform this operation. By default, only the bucket owner can perform this operation. The bucket owner can allow other users to perform this operation by granting them the permission or setting a bucket policy.

When a bucket has a default storage class, if users do not specify the object storage class when uploading or copying an object or initializing a multipart upload task, the object will use the default bucket storage class.

When users do not manually set a default storage class for a bucket, the bucket will have the Standard storage class by default.

Request Syntax
--------------

.. code-block:: text

   PUT /?storagePolicy HTTP/1.1
   User-Agent: agent
   Host: bucketname.obs.example.com
   Date: date
   Accept: */*
   Date: date
   Authorization: authorization
   Content-Length: length

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <StoragePolicy xmlns="http://obs.example.com/doc/2015-06-30/">
     <DefaultStorageClass>STANDARD</DefaultStorageClass>
   </StoragePolicy>

Request Parameters
------------------

This request involves no parameters.

Request Headers
---------------

This request uses common headers. For details about common request headers, see :ref:`Common Request Headers <en-us_topic_0125560462>`.

Request Elements
----------------

This request uses elements to specify the default bucket storage class. :ref:`Table 1 <en-us_topic_0125560403__table63485364>` describes the elements.

.. _en-us_topic_0125560403__table63485364:

.. table:: **Table 1** Request elements

   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Element               | Description                                                                                                                                                                          | Remarks               |
   +=======================+======================================================================================================================================================================================+=======================+
   | DefaultStorageClass   | Indicates the default bucket storage class.                                                                                                                                          | Mandatory             |
   |                       |                                                                                                                                                                                      |                       |
   |                       | It is a character string and can be **STANDARD** (OBS Standard), **STANDARD_IA** (OBS Warm), or **GLACIER** (OBS Cold). Note that the three storage class values are case-sensitive. |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
   Server: Server Name
   x-amz-request-id: request id
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   x-amz-id-2: id
   Date: date
   Content-Length: 0

Response Headers
----------------

This response uses common headers. For details about common response headers, see :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   PUT /?storagePolicy HTTP/1.1
   User-Agent: Jakarta Commons-HttpClient/3.1
   Host: bucketname.obs.example.com
   Accept: */*
   Date: Sun, 26 Sep 2017 08:24:46 GMT
   Authorization: AWS 04RZT432N80TGDF2Y2G2:ZyEGq367GyGGyItzr5egJOjaqiM=
   Content-Length: 240
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <StoragePolicy xmlns="http://obs.example.com/doc/2015-06-30/">
     <DefaultStorageClass>STANDARD</DefaultStorageClass>
   </StoragePolicy>

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
   Server: OBS
   x-amz-request-id: 3CEF0000015D08E1CF94AE61EA0EA1BC
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   x-amz-id-2: 0Z9Og4sWbGljhJq/UYfv6oBCwQ3/ZidsCQYz4CYBU305KRQnMwJWNXk/3/vswTEx
   Date: Sun, 26 Sep 2017 08:28:06 GMT
   Content-Length: 0

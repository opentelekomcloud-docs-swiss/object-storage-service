:original_name: en-us_topic_0125560378.html

.. _en-us_topic_0125560378:

GET Bucket storage class
========================

You can use this operation to obtain the default storage class of a bucket.

Only users granted the **s3:GetBucketStoragePolicy** permission can perform this operation. By default, only the bucket owner can perform this operation. The bucket owner can allow other users to perform this operation by granting them the permission or setting a bucket policy.

Request Syntax
--------------

.. code-block:: text

   GET /?storagePolicy HTTP/1.1
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

This request uses common headers. For details about common request headers, see :ref:`Common Request Headers <en-us_topic_0125560462>`.

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

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <StoragePolicy xmlns="http://obs.example.com/doc/2015-06-30/">
     <DefaultStorageClass>STANDARD</DefaultStorageClass>
   </StoragePolicy>

Response Headers
----------------

This response uses common headers. For details about common response headers, see :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response contains elements to specify the default bucket storage class. :ref:`Table 1 <en-us_topic_0125560378__table40100219>` describes the elements.

.. _en-us_topic_0125560378__table40100219:

.. table:: **Table 1** Response elements

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                          |
   +===================================+======================================================================================================================+
   | StoragePolicy                     | Indicates the bucket storage specification, including the default bucket storage class.                              |
   |                                   |                                                                                                                      |
   |                                   | Type: XML                                                                                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------+
   | DefaultStorageClass               | Indicates the default bucket storage class.                                                                          |
   |                                   |                                                                                                                      |
   |                                   | Type: It is a character string. :ref:`Table 1 <en-us_topic_0125560403__table63485364>` provides the possible values. |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

No special error responses are returned. For details about error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   GET /?storagePolicy HTTP/1.1
   User-Agent: Jakarta Commons-HttpClient/3.1
   Host: bucketname.obs.example.com
   Accept: */*
   Date: Sun, 26 Sep 2017 08:24:46 GMT
   Authorization: AWS 08350B985315591007AD:UpIi7+loQpsAFUpKCYvmIuZyFP0=

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
   Server: OBS
   x-amz-request-id: 3CEF0000015D0B5293440F668629A2C9
   x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
   x-amz-id-2: Dbn8aLu3MP7QA692G1pQdYZTf3Xa7vVGikDMbX+VfLFhat/ML3I/YkW8fwvWQSNr
   Content-Type: application/xml
   Date: Sun, 26 Sep 2017 08:24:47 GMT
   Content-Length: 187

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <StoragePolicy xmlns="http://obs.example.com/doc/2015-06-30/">
     <DefaultStorageClass>STANDARD</DefaultStorageClass>
   </StoragePolicy>

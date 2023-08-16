:original_name: en-us_topic_0125560486.html

.. _en-us_topic_0125560486:

Upload Part
===========

After initiating a multipart upload, you can use this operation to upload parts for the multipart upload using its **uploadId**.

In a multipart upload for a specific object, parts of the object can be uploaded in any sequence and multiple parts can be uploaded concurrently.

Part sizes range from 5 MB to 5 GB. However, in a **complete multipart** operation, the size of the last uploaded part must range from 0 to 5 GB. In addition, the **uploadId** of each part must be in the range of 1 to 10000.

.. important::

   When the same multipart of the same object is uploaded concurrently, the server complies with the Last Write Win policy.

   The time of Last Write is the creation time of the multipart metadata. To ensure data security, you must add a lock to the client to ensure the upload consistency of the same multipart. There is no need to add a lock when different parts of the same object are uploaded.

Request Syntax
--------------

.. code-block:: text

   PUT /ObjectName?partNumber=partNum&uploadId=uploadID  HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Content-Length: Size
    Authorization: Signature
    Content-MD5: md5
    Expect: expect

Request Parameters
------------------

This request uses parameters to specify the ID of a multipart upload and part number. :ref:`Table 1 <en-us_topic_0125560486__table6481817>` describes the parameters.

.. _en-us_topic_0125560486__table6481817:

.. table:: **Table 1** Request parameters

   +-----------------------+---------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                       | Remarks               |
   +=======================+===================================================================================================+=======================+
   | partNumber            | Indicates the number that identifies a part to be uploaded. It can be any number from 1 to 10,000 | Mandatory             |
   |                       |                                                                                                   |                       |
   |                       | Type: Integer                                                                                     |                       |
   +-----------------------+---------------------------------------------------------------------------------------------------+-----------------------+
   | uploadId              | Indicates the ID of a multipart upload.                                                           | Mandatory             |
   |                       |                                                                                                   |                       |
   |                       | Type: String                                                                                      |                       |
   +-----------------------+---------------------------------------------------------------------------------------------------+-----------------------+

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
    x-amz-id-2: id
    x-amz-request-id: request id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Date: date
    ETag: etagValue
    Content-Length: length
    Server: server

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response involves no elements.

Error Responses
---------------

-  If the part number exceeds the range of 1 to 10,000, OBS returns status code **400 Bad Request**.
-  If the part size is greater than 5 GB, OBS returns status code **400 Bad Request**.
-  If an AK or signature is invalid, OBS returns status code **403 Forbidden** and error code **AccessDenied**.
-  If the requested bucket does not exist, OBS returns status code **404 Not Found** and error code **NoSuchBucket**.
-  If the requester does not have **READ** permission for the requested bucket, OBS returns status code **403 Forbidden** and error code **AccessDenied**.
-  If the requested multipart upload does not exist, OBS returns status code **404 Not Found** and error code **NoSuchUpload**.
-  If the requester is not the initiator of the multipart upload, OBS returns status code **403 Forbidden** and error code **AccessDenied**.

For details about other error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   PUT /ObjectName?partNumber=1&uploadId=VCVsb2FkIElEIGZvciBlbZZpbmcncyBteS1tb3ZpZS5tMnRzIHVwbG9hZR  HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Mon, 1 Nov 2010 20:34:56 GMT
    Content-Length: 1048596
    Authorization:AWS 14RZT432N80TGDF2Y2G2:8se2hm3YLchJhuPMDrybeITcuo0=
    Content-MD5:q3q7DaS8pTI6thGbtdzSlg==

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    x-amz-id-2: Vvag1LuByRx9e6j5Onimru9pO4ZVKnJ2Qz7/C1NPcfTWAtRPfTaOFg==
    x-amz-request-id: 656c76696e6727732072657175657374
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Date: Mon, 1 Nov 2010 20:34:56 GMT
    ETag: "b54357faf0632cce46e942fa68356b38"
    Content-Length: 1048596

:original_name: en-us_topic_0125560338.html

.. _en-us_topic_0125560338:

Complete Multipart Upload
=========================

After uploading all parts for a multipart upload, you can use this operation to complete the multipart upload.

Upon receiving a Complete Multipart Upload request, OBS concatenates the specified parts to create a new object. All associated parts cannot be downloaded until the multipart upload is complete.

When starting to complete a multipart upload, OBS first copies the header information from the metadata of associated parts and then incorporates the header information into the metadata of the newly created object.

Before a multipart upload is completed, all associated parts occupy storage quota. After the multipart upload is completed, only parts included in the part list specified in the **Complete Multipart Upload** request are concatenated. These parts still occupy storage quota while other parts are deleted to release storage quota.

After a multipart upload is completed, you can send a **GET** request to obtain the newly created object or some parts comprising this object by specifying a range in the request. You can also send a **DELETE** request to delete all parts uploaded for the multipart upload. The deleted parts cannot be restored.

The MD5 value recorded in the ETag of a newly created object is calculated using the MD5 values of the parts comprising this object. The object ETag is calculated as follows:

*MD5(M\ 1\ M\ 2......M\ N)-N*

where

**M\ n** is the MD5 value of part N

**N** is the total number of parts

Versioning
----------

If a bucket has versioning enabled, a unique version ID is generated for an object created from a multipart upload in this bucket and the version ID is returned in response header **x-amz-version-id**. If the bucket has versioning suspended, the version ID of the object is **null**. For details about bucket versioning, see section :ref:`PUT Bucket versioning <en-us_topic_0125560444>`.

.. important::

   If 10 parts are uploaded but only 9 parts are selected for combination, the part that is not combined will be automatically deleted. After the part is deleted, it cannot be restored. Before combining the parts, adopt the interface used to list the parts that have been uploaded to check all parts to ensure that no part is missed.

Request Syntax
--------------

.. code-block:: text

   POST /ObjectName?uploadId=uploadID HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    Content-Length: length
    Authorization: auth
    Expect: expect
    <CompleteMultipartUpload>
    <Part>
    <PartNumber>partNum1</PartNumber>
    <ETag>etag1</ETag>
    </Part>
    <Part>
    <PartNumber>partNum2</PartNumber>
    <ETag>etag2</ETag>
    </Part>
    <Part>
    <PartNumber>partNum3</PartNumber>
    <ETag>etag3</ETag>
    </Part>
    </CompleteMultipartUpload>

Request Parameters
------------------

This request uses one parameter to specify the ID of the multipart upload to be completed. :ref:`Table 1 <en-us_topic_0125560338__table6473820>` describes the parameter.

.. _en-us_topic_0125560338__table6473820:

.. table:: **Table 1** Request parameter

   +-----------------------+-----------------------------------------------------------+-----------------------+
   | Parameter             | Description                                               | Remarks               |
   +=======================+===========================================================+=======================+
   | uploadId              | Indicates the ID of the multipart upload to be completed. | Mandatory             |
   |                       |                                                           |                       |
   |                       | Type: String                                              |                       |
   +-----------------------+-----------------------------------------------------------+-----------------------+

Request Headers
---------------

This request uses common headers. For details about common request headers, see section :ref:`Common Request Headers <en-us_topic_0125560462>`.

Request Elements
----------------

This request contains elements to specify the part list for the multipart upload to be completed. :ref:`Table 2 <en-us_topic_0125560338__table57330131>` describes the elements.

.. _en-us_topic_0125560338__table57330131:

.. table:: **Table 2** Request elements

   +-------------------------+-------------------------------------------------------------------+-----------------------+
   | Element                 | Description                                                       | Remarks               |
   +=========================+===================================================================+=======================+
   | CompleteMultipartUpload | Indicates the container for the list of parts to be concatenated. | Mandatory             |
   |                         |                                                                   |                       |
   |                         | Type: XML                                                         |                       |
   +-------------------------+-------------------------------------------------------------------+-----------------------+
   | PartNumber              | Indicates the number that identifies a part.                      | Mandatory             |
   |                         |                                                                   |                       |
   |                         | Type: Integer                                                     |                       |
   +-------------------------+-------------------------------------------------------------------+-----------------------+
   | ETag                    | Indicates the ETag returned after a part is uploaded.             | Mandatory             |
   |                         |                                                                   |                       |
   |                         | Type: String                                                      |                       |
   +-------------------------+-------------------------------------------------------------------+-----------------------+

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
    x-amz-id-2: id
    x-amz-request-id: request id
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-reserved-indicator: indicator
    Content-Type: type
    Date: date
    Connection: state
    Server: server
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <CompleteMultipartUploadResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <Location>http://example-Bucket.obs.example.com/example-Object</Location>
    <Bucket>BucketName</Bucket>
    <Key>ObjectName</Key>
    <ETag>ETag</ETag>
    </CompleteMultipartUploadResult>

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

This response also uses one optional header, as described in :ref:`Table 3 <en-us_topic_0125560338__table49929783>`.

.. _en-us_topic_0125560338__table49929783:

.. table:: **Table 3** Optional response header

   +-----------------------------------+-------------------------------------------------------------------------+
   | Header                            | Description                                                             |
   +===================================+=========================================================================+
   | x-amz-version-id                  | Indicates the version ID of the object created from a multipart upload. |
   |                                   |                                                                         |
   |                                   | Type: String                                                            |
   +-----------------------------------+-------------------------------------------------------------------------+

Response Elements
-----------------

This response contains elements to indicate the results of completing a multipart upload. :ref:`Table 4 <en-us_topic_0125560338__table32583578>` describes the elements.

.. _en-us_topic_0125560338__table32583578:

.. table:: **Table 4** Response elements

   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                                                                             |
   +===================================+=========================================================================================================================================================================+
   | Location                          | Indicates the URL of the newly created object.                                                                                                                          |
   |                                   |                                                                                                                                                                         |
   |                                   | Type: String                                                                                                                                                            |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Bucket                            | Indicates the bucket that contains the newly created object.                                                                                                            |
   |                                   |                                                                                                                                                                         |
   |                                   | Type: String                                                                                                                                                            |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key                               | Indicates the key of the newly created object.                                                                                                                          |
   |                                   |                                                                                                                                                                         |
   |                                   | Type: String                                                                                                                                                            |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ETag                              | Indicates the ETag that identifies the metadata of the newly created object. This ETag is calculated using the MD5 values of parts comprising the newly created object. |
   |                                   |                                                                                                                                                                         |
   |                                   | Type: String                                                                                                                                                            |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

-  If the request contains no request body, OBS returns status code **400 Bad Request**.
-  If the request contains a request body in incorrect syntax, OBS returns status code **400 Bad Request**.
-  If parts are not listed in the request body in ascending order, OBS returns status code **400 Bad Request** and error code **InvalidPartOrder**.
-  If an AK or signature is invalid, OBS returns status code **403 Forbidden** and error code **AccessDenied**.
-  If the requested bucket does not exist, OBS returns status code **404 Not Found** and error code **NoSuchBucket**.
-  If the requested multipart upload does not exist, OBS returns **404 NotFound** and error code **NoSuchUpload**.
-  If the requester is not the initiator of the multipart upload, OBS returns status code **403 Forbidden** and error code **AccessDenied**.
-  If the part list contains nonexistent parts, OBS returns status code **400 Bad Request** and error code **InvalidPart**.
-  If the ETag of a part in the part list is incorrect, OBS returns status code **400 Bad Request** and error code **InvalidPart**.
-  If the size of a part (excluding the last part) in the part list is smaller than 5 MB, OBS returns status code **400 Bad Request**.
-  If the size of the newly created object is greater than 48.8 TB, OBS returns status code **400 Bad Request**.

For details about other error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   POST /example-object?uploadId=AAAsb2FkIElEIGZvciBlbHZpbmcncyWeeS1tb3ZpZS5tMnRzIRRwbG9hZA HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Mon, 1 Nov 2010 20:34:56 GMT
    Content-Length: 391
    Authorization: AWS AKIAIOSFODNN7EXAMPLE:0RQf4/cRonhpaBX5sCYVf1bNRuU=
    Expect: 100-continue
    <CompleteMultipartUpload>
    <Part>
    <PartNumber>1</PartNumber>
    <ETag>"a54357aff0632cce46d942af68356b38"</ETag>
    </Part>
    <Part>
    <PartNumber>2</PartNumber>
    <ETag>"0c78aef83f66abc1fa1e8477f296d394"</ETag>
    </Part>
    <Part>
    <PartNumber>3</PartNumber>
    <ETag>"acbd18db4cc2f85cedef654fccc4a4d8"</ETag>
    </Part>
    </CompleteMultipartUpload>

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    x-amz-id-2: Uuag1LuByRx9e6j5Onimru9pO4ZVKnJ2Qz7/C1NPcfTWAtRPfTaOFg==
    x-amz-request-id: 656c76696e6727732072657175657374
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-reserved-indicator: 3
    Content-Type: application/xml
    Date: Mon, 1 Nov 2010 20:34:56 GMT
    Connection: close
    Content-Length: 306
    Server: OBS
   <?xml version="1.0" encoding="UTF-8"?>
    <CompleteMultipartUploadResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <Location>http://example-Bucket.obs.example.com/example-Object</Location>
    <Bucket>Example-Bucket</Bucket>
    <Key>Example-Object</Key>
    <ETag>"3858f62230ac3c915f300c664312c11f-9"</ETag>
    </CompleteMultipartUploadResult>

Sample Request (Getting an Object Created from a Multipart Upload with Version ID Specified)
--------------------------------------------------------------------------------------------

.. code-block::

    POST /object?uploadId=DCD2FC9CAB7800000143947AB58A5094 HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Wed, 15 Jan 2014 06:09:39 +0000
    Authorization: AWS C9590CEB8EC051BDEC9D:xQ9EFib6cohqMu2bLLJ0soseeUI=
    Content-Length: 155
    Expect: 100-continue
    <CompleteMultipartUpload>
    <Part>
    <PartNumber>1</PartNumber>
    <ETag>"9fd2e548507ceef1a2183a8328b5cf2c"</ETag>
    </Part>
    </CompleteMultipartUpload>

Sample Response (Getting an Object Created from a Multipart Upload with Version ID Specified)
---------------------------------------------------------------------------------------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-request-id: DCD2FC9CAB78000001439484FB045617
    x-amz-id-2: xw5X6Y7YIpWnQgHNYG3ce4+lj8O1GjiGvFXSgdPV1x2tYn2iZXFnTJm0yh5X5XnV
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    x-reserved-indicator: 3
    Content-Type: application/xml
    x-amz-version-id: AAABQ5R6tZ7c0vycq3gAAAAbVURTRkha
    Date: Wed, 15 Jan 2014 06:09:39 GMT
    Content-Length: 300
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <CompleteMultipartUploadResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <Location>/example/multi</Location>
    <Bucket>example</Bucket>
    <Key>multi</Key>
    <ETag>"59297fcb0de64c706cbb46e382d9c625-1"</ETag>
    </CompleteMultipartUploadResult>

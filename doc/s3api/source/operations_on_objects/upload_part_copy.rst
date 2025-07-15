:original_name: en-us_topic_0125560361.html

.. _en-us_topic_0125560361:

Upload Part - Copy
==================

After initiating a multipart upload, you can send an **Upload Part** request to upload parts for the multipart upload using its **uploadId**. The **Upload Part - Copy** operation allows you to upload a part by copying data from an existing object as data source.

.. important::

   You cannot determine whether a request is executed successfully only using **status_code** in the header returned by HTTP.

   If **200** in **status_code** is returned, the server has received the request and starts to process the request from the upload part. The body in the response shows whether the upload operation succeeds. The upload operation succeeds only when the body has ETags. Otherwise, the upload operation fails.

   Copy the source object as **part1**. If part1 already exists before you copy the source object, the old **part1** will be overwritten by the new **part1**.

   After the source object is copied, only the latest **part1** is listed. The old **part1** will be deleted. Before using the copy interface, ensure that the target part does not exist or is useless to avoid incorrect data deletion.

   During the copy process, the source object is not changed.

OBS Cold Objects
----------------

If source objects are OBS cold objects, check the restore status of the objects. You can copy the OBS cold objects only after the objects are restored. If the objects are not restored or are being restored, the copy fails, and error "403 Forbidden" is returned. The fault is described as follows:

ErrorCode: InvalidObjectState

ErrorMessage: Operation is not valid for the source object's storage class

Request Syntax
--------------

.. code-block:: text

   PUT /ObjectName?partNumber=partNum&uploadId=UploadID HTTP/1.1
    User-Agent: agent
    Host: bucketname.obs.example.com
    Accept: */*
    Date: date
    x-amz-copy-source: sourceobject
    x-amz-copy-source-range:bytes=start-end
    Authorization: auth
    Content-Length: length

Request Parameters
------------------

This request uses parameters to specify the ID of a multipart upload and part number. :ref:`Table 1 <en-us_topic_0125560361__table12334196>` describes the parameters.

.. _en-us_topic_0125560361__table12334196:

.. table:: **Table 1** Request parameters

   +-----------------------+-------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                 | Remarks               |
   +=======================+=============================================================+=======================+
   | partNumber            | Indicates the number that identifies a part to be uploaded. | Mandatory             |
   |                       |                                                             |                       |
   |                       | Type: Integer                                               |                       |
   +-----------------------+-------------------------------------------------------------+-----------------------+
   | uploadId              | Indicates the ID of a multipart upload.                     | Mandatory             |
   |                       |                                                             |                       |
   |                       | Type: String                                                |                       |
   +-----------------------+-------------------------------------------------------------+-----------------------+

Request Headers
---------------

This request uses headers listed in :ref:`Table 2 <en-us_topic_0125560361__table6620500>` in addition to common headers.

.. _en-us_topic_0125560361__table6620500:

.. table:: **Table 2** Request headers

   +-------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | Header                  | Description                                                                                                                                                                        | Remarks                                                                          |
   +=========================+====================================================================================================================================================================================+==================================================================================+
   | x-amz-copy-source       | Indicates the source object to be copied.                                                                                                                                          | Mandatory                                                                        |
   |                         |                                                                                                                                                                                    |                                                                                  |
   |                         | Type: String                                                                                                                                                                       |                                                                                  |
   +-------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-copy-source-range | Indicates the range of bytes (start-end) to be copied from the source object. **start** indicates the start byte of the part to be copied and **end** indicates the end byte.      | Optional                                                                         |
   |                         |                                                                                                                                                                                    |                                                                                  |
   |                         | Type: Integer                                                                                                                                                                      |                                                                                  |
   +-------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | x-amz-security-token    | Header field used to identify the request of a federated user. When the federal authentication function is enabled, users sending such requests are identified as federated users. | Optional. This parameter must be carried in the request sent by federated users. |
   |                         |                                                                                                                                                                                    |                                                                                  |
   |                         | Type: string                                                                                                                                                                       |                                                                                  |
   +-------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+

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
    Content-Type: type
    Date: date
    Server: server
    Transfer-Encoding: chunked

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <CopyPartResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <LastModified>modifiedDate</LastModified>
    <ETag>etagValue</ETag>
    </CopyPartResult>

Response Headers
----------------

This response uses common headers. For details about common response headers, see section :ref:`Common Response Headers <en-us_topic_0125560484>`.

Response Elements
-----------------

This response contains elements to indicate the copy results. :ref:`Table 3 <en-us_topic_0125560361__table44628158>` describes the elements.

.. _en-us_topic_0125560361__table44628158:

.. table:: **Table 3** Response elements

   +-----------------------------------+------------------------------------------------+
   | Element                           | Description                                    |
   +===================================+================================================+
   | LastModified                      | Indicates the date the part was last modified. |
   |                                   |                                                |
   |                                   | Type: String                                   |
   +-----------------------------------+------------------------------------------------+
   | ETag                              | Indicates the ETag of the source part.         |
   |                                   |                                                |
   |                                   | Type: String                                   |
   +-----------------------------------+------------------------------------------------+

Error Responses
---------------

-  If an AccessKey or signature is invalid, OBS returns status code **403 Forbidden** and error code **AccessDenied**.
-  If the requested bucket does not exist, OBS returns status code **404 Not Found** and error code **NoSuchBucket**.
-  If the requested source object does not exist, OBS returns status code **404 Not Found** and error code **NoSuchKey**.
-  If the requester does not have **READ** permission for the requested bucket, OBS returns status code **403 Forbidden** and error code **AccessDenied**.
-  If the requester does not have **WRITE** permission for the requested bucket, OBS returns status code **403 Forbidden** and error code **AccessDenied**.
-  If the requested multipart upload does not exist, OBS returns status code **404 Not Found** and error code **NoSuchUpload**.
-  If the requester is not the initiator of the multipart upload, OBS returns status code **403 Forbidden** and error code **AccessDenied**.
-  If the part size is greater than 5 GB, OBS returns status code **400 Bad Request**.
-  If the part number exceeds the range of 1 to 10,000, OBS returns status code **400 Bad Request**.

For details about other error responses, see :ref:`Table 1 <en-us_topic_0125560440__table30733758>`.

Sample Request
--------------

.. code-block:: text

   PUT /newobject?partNumber=1&uploadId=VCVsb2FkIElEIGZvciBlbZZpbmcncyBteS1tb3ZpZS5tMnRzIHVwbG9hZR HTTP/1.1
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: bucketname.obs.example.com
    Accept: */*
    Date: Mon, 11 Apr 2011 20:34:56 GMT
    x-amz-copy-source: /source-bucket/sourceobject
    x-amz-copy-source-range:bytes=500-6291456
    Authorization: AWS AKIAIOSFODNN7EXAMPLE:VGhpcyBtZXNzYWdlIHNpZ25lZGGieSRlbHZpbmc=
    Content-Length: 5120

Sample Response
---------------

.. code-block::

   HTTP/1.1 200 OK
    Server: OBS
    x-amz-id-2: Vvag1LuByRx9e6j5Onimru9pO4ZVKnJ2Qz7/C1NPcfTWAtRPfTaOFg==
    x-amz-request-id: 656c76696e6727732072657175657374
    x-reserved: amazon, aws and amazon web services are trademarks or registered trademarks of Amazon Technologies, Inc
    Content-Type: application/xml
    Date: Mon, 11 Apr 2011 20:34:56 GMT
    Transfer-Encoding: chunked

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <CopyPartResult xmlns="http://obs.example.com/doc/2015-06-30/">
    <LastModified>2009-10-28T22:32:00</LastModified> <ETag>"9b2cf535f27731c974343645a3985328"</ETag>
    </CopyPartResult>

:original_name: obs_04_0100.html

.. _obs_04_0100:

Copying Parts
=============

Functions
---------

After creating a multipart upload job, you can specify its upload ID and upload a part to the job in OBS. Alternatively, you can make an API call to add a part (part of an object or the whole object).

.. important::

   You cannot determine whether a request is successful only based on the **status_code** in the returned HTTP header. If **200** is returned for **status_code**, the server has received the request and started to process the request. The copy is successful only when the body in the response contains ETag.

Copy the source object and save it as **part1**. If a **part1** already exists before the copying, the original **part1** will be overwritten by the newly copied **part1**. After the copy is successful, only the latest **part1** is displayed. The old **part1** data will be deleted. Therefore, ensure that the target part does not exist or has no value when using the part copy operation. Otherwise, data may be deleted by mistake. The source object in the copy process does not change.

Request Syntax
--------------

.. code-block:: text

   PUT /ObjectName?partNumber=partNum&uploadId=UploadID HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   x-obs-copy-source: sourceobject
   x-obs-copy-source-range:bytes=start-end
   Authorization: authorization
   Content-Length: length

Request Parameters
------------------

To copy a part, you need to specify the part number of the target part and the multipart upload task number. :ref:`Table 1 <obs_04_0100__table12334196>` describes the parameters.

.. _obs_04_0100__table12334196:

.. table:: **Table 1** Request parameters

   +-----------------------+--------------------------------------------+-----------------------+
   | Parameter             | Description                                | Mandatory             |
   +=======================+============================================+=======================+
   | partNumber            | Indicates the ID of a part to be uploaded. | Yes                   |
   |                       |                                            |                       |
   |                       | Type: integer                              |                       |
   +-----------------------+--------------------------------------------+-----------------------+
   | uploadId              | Indicates a multipart upload ID.           | Yes                   |
   |                       |                                            |                       |
   |                       | Type: string                               |                       |
   +-----------------------+--------------------------------------------+-----------------------+

Request Headers
---------------

In addition the common message headers, the request uses two extended headers. :ref:`Table 3 <obs_04_0007__table25197309>` describes the common message header.

.. table:: **Table 2** Request headers

   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Header                  | Description                                                                                                                                                                     | Mandatory             |
   +=========================+=================================================================================================================================================================================+=======================+
   | x-obs-copy-source       | Indicates the source object to be copied.                                                                                                                                       | Yes                   |
   |                         |                                                                                                                                                                                 |                       |
   |                         | Type: string                                                                                                                                                                    |                       |
   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | x-obs-copy-source-range | Indicates the range of bytes (start - end) to be copied from the source object. **start** indicates the start byte of the part to be copied and **end** indicates the end byte. | No                    |
   |                         |                                                                                                                                                                                 |                       |
   |                         | Type: integer                                                                                                                                                                   |                       |
   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

Request Elements
----------------

This request involves no elements.

Response Syntax
---------------

.. code-block::

   HTTP/1.1 status_code
   Date: date

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <CopyPartResult xmlns="http://obs.region.example.com/doc/2015-06-30/">
       <LastModified>modifiedDate</LastModified>
       <ETag>etag</ETag>
   </CopyPartResult>

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains elements of a part copy result. :ref:`Table 3 <obs_04_0100__table44628158>` describes the elements.

.. _obs_04_0100__table44628158:

.. table:: **Table 3** Response elements

   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                                                               |
   +===================================+===========================================================================================================================================+
   | LastModified                      | Indicates the latest time an object was modified.                                                                                         |
   |                                   |                                                                                                                                           |
   |                                   | Type: string                                                                                                                              |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | ETag                              | ETag value of the target part. It is the unique identifier of the part content and is used to verify data consistency when merging parts. |
   |                                   |                                                                                                                                           |
   |                                   | Type: string                                                                                                                              |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+

Error Responses
---------------

#. If the AK or signature is invalid, OBS returns **403 Forbidden** and the error code is **AccessDenied**.
#. Check whether the source bucket or destination bucket exists. If the source bucket or destination bucket does not exist, OBS returns **404 Not Found** and the error code is **NoSuchBucket**.
#. If the source object does not exist, OBS returns **404 Not Found** and the error code is **NoSuchKey**.
#. If the user does not have the read permission for the specified object, OBS returns **403 Forbidden** and the error code is **AccessDenied**.
#. If the user does not have the write permission for the destination bucket, OBS returns **403 Forbidden** and the error code is **AccessDenied**.
#. If the specified task does not exist, OBS returns **404 Not Found** and the error code is **NoSuchUpload**.
#. If the user is not the initiator of the multipart upload task, OBS returns **403 Forbidden** and the error code is **AccessDenied**.
#. When the size of a copied part has exceeded 5 GB, OBS returns **400 Bad Request**.
#. If a part number is not within the range from 1 to 10000, OBS returns error code **400 Bad Request**.

Other errors are included in :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   PUT /tobject02?partNumber=2&uploadId=00000163D40171ED8DF4050919BD02B8 HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 05:16:32 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:dSnpnNpawDSsLg/xXxaqFzrAmMw=
   x-obs-copy-source: /destbucket/object01

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: 8DF400000163D40ABBD20405D30B0542
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCTIJpD2efLy5o8sTTComwBb2He0j11Ne
   Content-Type: application/xml
   Date: WED, 01 Jul 2015 05:16:32 GMT
   Transfer-Encoding: chunked

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <CopyPartResult xmlns="http://obs.example.com/doc/2015-06-30/">
     <LastModified>2015-07-01T05:16:32.344Z</LastModified>
     <ETag>"3b46eaf02d3b6b1206078bb86a7b7013"</ETag>
   </CopyPartResult>

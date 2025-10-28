:original_name: obs_04_0099.html

.. _obs_04_0099:

Uploading Parts
===============

Functions
---------

After a multipart upload task is created, you can upload parts for this task using the obtained multipart upload ID. When parts are uploaded in a multipart upload of an object, the upload sequence does not affect part merging, namely, multiple parts can be uploaded concurrently.

Ensure that the part size ranges from 100 KB to 5 GB and the size of the last part ranges from 0 to 5 GB. Otherwise, an error will be reported when you assemble parts. The upload part ID ranges from 1 to 10,000.

.. important::

   The value of **partNumber** in a multipart task is unique. If you upload a part of the same **partNumber** repeatedly, the last part uploaded will overwrite the previous one. When multiple concurrent uploading of the same **partNumber** part of the same object is performed, the Last Write Win policy is applied. The time of **Last Write** is defined as the time when the metadata of the part is created. To ensure data accuracy, the client must be locked to ensure concurrent upload of the same part of the same object. Concurrent upload of different parts of the same object does not need to be locked.

Request Syntax
--------------

.. code-block:: text

   PUT /ObjectName?partNumber=partNum&uploadId=uploadID  HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Content-Length: length
   Authorization: authorization
   Content-MD5:md5
   <object Content>

Request Parameters
------------------

This request uses parameters to specify the upload task ID and part number. :ref:`Table 1 <obs_04_0099__table8720142719451>` describes the parameters.

.. _obs_04_0099__table8720142719451:

.. table:: **Table 1** Request parameters

   +-----------------+-----------------+--------------------+--------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                |
   +=================+=================+====================+============================================+
   | partNumber      | Integer         | Yes                | **Definition**:                            |
   |                 |                 |                    |                                            |
   |                 |                 |                    | Indicates the ID of a part to be uploaded. |
   |                 |                 |                    |                                            |
   |                 |                 |                    | **Constraints**:                           |
   |                 |                 |                    |                                            |
   |                 |                 |                    | None                                       |
   |                 |                 |                    |                                            |
   |                 |                 |                    | **Range**:                                 |
   |                 |                 |                    |                                            |
   |                 |                 |                    | An integer ranging from 1 to 10000.        |
   |                 |                 |                    |                                            |
   |                 |                 |                    | **Default value**:                         |
   |                 |                 |                    |                                            |
   |                 |                 |                    | None                                       |
   +-----------------+-----------------+--------------------+--------------------------------------------+
   | uploadId        | String          | Yes                | **Definition**:                            |
   |                 |                 |                    |                                            |
   |                 |                 |                    | Indicates a multipart upload ID.           |
   |                 |                 |                    |                                            |
   |                 |                 |                    | **Constraints**:                           |
   |                 |                 |                    |                                            |
   |                 |                 |                    | None                                       |
   |                 |                 |                    |                                            |
   |                 |                 |                    | **Range**:                                 |
   |                 |                 |                    |                                            |
   |                 |                 |                    | None                                       |
   |                 |                 |                    |                                            |
   |                 |                 |                    | **Default value**:                         |
   |                 |                 |                    |                                            |
   |                 |                 |                    | None                                       |
   +-----------------+-----------------+--------------------+--------------------------------------------+

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Request Elements
----------------

This request involves no elements.

Response Syntax
---------------

::

   HTTP/1.1 status_code
   Date: date
   ETag: etag
   Content-Length: length

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

Response Elements
-----------------

This response contains no elements.

Error Responses
---------------

#. If a part number is not within the range from 1 to 10000, OBS returns **400 Bad Request**.
#. If a part size has exceeded 5 GB, the error code **400 Bad Request** is returned.
#. If the AK or signature is invalid, OBS returns **403 Forbidden** and the error code is **AccessDenied**.
#. Check whether the bucket exists. If the bucket is not found, OBS returns **404 Not Found** and the error code is **NoSuchBucket**.
#. View the bucket ACL to check whether the user has the read permission for the requested bucket. If the user does not have the read permission, OBS returns **403 AccessDenied**.
#. Check whether the multipart upload task exists. If the task does not exist, OBS returns **404 Not Found** and the error code is **NoSuchUpload**.
#. Check whether the request user is the initiator of the multipart upload task. If not, OBS returns **403 Forbidden** and the error code is **AccessDenied**.

Other errors are included in :ref:`Table 2 <obs_04_0115__d0e843>`.

Sample Request
--------------

.. code-block:: text

   PUT /object02?partNumber=1&uploadId=00000163D40171ED8DF4050919BD02B8 HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 05:15:55 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:ZB0hFwaHubi1aKHv7dSZjJts40g=
   Content-Length: 102015348

   [102015348 Byte part content]

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: 8DF400000163D40956A703289CA066F1
   ETag: "b026324c6904b2a9cb4b88d6d61c81d1"
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCUQu/EOEVSMa04GXVwy0z9WI+BsDKvfh
   Date: WED, 01 Jul 2015 05:15:55 GMT
   Content-Length: 0

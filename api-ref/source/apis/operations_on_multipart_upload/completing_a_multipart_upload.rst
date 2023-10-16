:original_name: obs_04_0102.html

.. _obs_04_0102:

Completing a Multipart Upload
=============================

Functions
---------

After uploading all parts for a multipart upload, you can use this operation to complete the multipart upload. Before performing this operation, you cannot download the uploaded data. When merging parts, you need to copy the additional message header information recorded during the initialization of the multipart upload task to the object metadata. The processing process is the same as that of the common upload object with these message headers. In the case of merging parts concurrently, the Last Write Win policy must be followed but the time for initiating Last Write is specified as the time when a part multipart upload is initiated.

If a multipart upload has not been aborted, the uploaded parts occupy your storage quota. After all parts in the multipart upload are merged to an object, only the object occupies your storage quota. If a part uploaded in a multipart upload is not used in any merging parts multipart uploads, the part will be deleted to release storage quota.

You can send a request for downloading all or some data of the generated multipart by specifying a range.

You can send a request for deleting all parts uploaded in a multipart upload. Deleted data cannot be restored.

The merged parts do not use the MD5 value of entire object as the ETag. Their ETag is calculated as follows: *MD5(M\ 1\ M\ 2...M\ N)-N*, where *M\ n* is the MD5 value of part *n* (*N* is the total number of parts). As described in the :ref:`Sample Request <obs_04_0102__section74706439232>`, there are three parts and each part has an MD5 value. The MD5 values of the three parts are recalculated to obtain a new MD5 value. Then *-N* is added to the right of the MD5 value to get the ETag of the combined parts. In this example, *-N* is **-3**.

If the response to an object merge request times out and error 500 or 503 is returned, you can first obtain the object metadata of the multipart upload task. Then, check whether the value of header **x-obs-uploadId** in the response is the same as the ID of this multipart upload task. If they are the same, object parts have been successfully merged on the server and you do not need to try again. For details, see :ref:`Consistency of Concurrent Operations <obs_04_0118>`.

WORM
----

If a bucket has WORM enabled, the WORM protection will be automatically applied to the object generated after a multipart upload is complete. If you specify WORM headers and a retention expiration date when you initiate a multipart upload, the protection for the assembled object ends on the specified date. If you do not specify WORM headers during the initiation, but have configured the default bucket-level retention policy, this default policy is automatically applied and the protection starts when the multipart upload is complete. After a multipart upload is complete, you can still configure object-level WORM retention policies for the assembled object.

Versioning
----------

If a bucket has versioning enabled, a unique version ID is generated for an object created from a multipart upload in this bucket and the version ID is returned in response header **x-obs-version-id**. If versioning is suspended for a bucket, the object version obtained after the merge is **null**. For details about the versioning statuses of a bucket, see :ref:`Configuring Versioning for a Bucket <obs_04_0037>`.

.. important::

   If 10 parts are uploaded but only nine parts are selected for merge, the parts that are not merged will be automatically deleted by the system. The parts that are not merged cannot be restored after being deleted. Before combining the parts, adopt the interface used to list the parts that have been uploaded to check all parts to ensure that no part is missed.

Request Syntax
--------------

.. code-block:: text

   POST /ObjectName?uploadId=uploadID HTTP/1.1
   Host: bucketname.obs.region.example.com
   Date: date
   Content-Length: length
   Authorization: authorization
   <CompleteMultipartUpload>
       <Part>
           <PartNumber>partNum</PartNumber>
           <ETag>etag</ETag>
       </Part>
       <Part>
           <PartNumber>partNum</PartNumber>
           <ETag>etag</ETag>
       </Part>
       <Part>
           <PartNumber>partNum</PartNumber>
           <ETag>etag</ETag>
       </Part>
   </CompleteMultipartUpload>

Request Parameters
------------------

This request uses parameters to specify the ID of a multipart upload whose parts will be merged. :ref:`Table 1 <obs_04_0102__table6473820>` describes the parameters.

.. _obs_04_0102__table6473820:

.. table:: **Table 1** Request parameters

   +-----------------------+-------------------------------+-----------------------+
   | Parameter             | Description                   | Mandatory             |
   +=======================+===============================+=======================+
   | uploadId              | Indicates a multipart upload. | Yes                   |
   |                       |                               |                       |
   |                       | Type: string                  |                       |
   +-----------------------+-------------------------------+-----------------------+

Request Headers
---------------

This request uses common headers. For details, see :ref:`Table 3 <obs_04_0007__table25197309>`.

Request Elements
----------------

This request uses elements to specify the list of parts to be merged. :ref:`Table 2 <obs_04_0102__table57330131>` describes the elements.

.. _obs_04_0102__table57330131:

.. table:: **Table 2** Request Elements

   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Element                 | Description                                                                                                                                                                     | Mandatory             |
   +=========================+=================================================================================================================================================================================+=======================+
   | CompleteMultipartUpload | List of parts to be combined                                                                                                                                                    | Yes                   |
   |                         |                                                                                                                                                                                 |                       |
   |                         | Type: XML                                                                                                                                                                       |                       |
   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | PartNumber              | Part number                                                                                                                                                                     | Yes                   |
   |                         |                                                                                                                                                                                 |                       |
   |                         | Type: integer                                                                                                                                                                   |                       |
   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | ETag                    | ETag value returned upon successful upload of a part. It is the unique identifier of the part content. This parameter is used to verify data consistency when parts are merged. | Yes                   |
   |                         |                                                                                                                                                                                 |                       |
   |                         | Type: string                                                                                                                                                                    |                       |
   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

Response Syntax
---------------

::

   HTTP/1.1 status_code
   Date: date
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <CompleteMultipartUploadResult xmlns="http://obs.region.example.com/doc/2015-06-30/">
       <Location>http://example-Bucket.obs.region.example.com/example-Object</Location>
       <Bucket>bucketname</Bucket>
       <Key>ObjectName</Key>
       <ETag>ETag</ETag>
   </CompleteMultipartUploadResult>

Response Headers
----------------

The response to the request uses common headers. For details, see :ref:`Table 1 <obs_04_0013__d0e686>`.

In addition to the common response headers, the message headers listed in :ref:`Table 3 <obs_04_0102__table31698209142128>` may be used.

.. _obs_04_0102__table31698209142128:

.. table:: **Table 3** Additional response headers

   +-----------------------------------+-------------------------------------------------+
   | Header                            | Description                                     |
   +===================================+=================================================+
   | x-obs-version-id                  | Version of the object after parts being merged. |
   |                                   |                                                 |
   |                                   | Type: string                                    |
   +-----------------------------------+-------------------------------------------------+

Response Elements
-----------------

This response uses elements to return the result of merging parts. :ref:`Table 4 <obs_04_0102__table32583578>` describes the elements.

.. _obs_04_0102__table32583578:

.. table:: **Table 4** Response elements

   +-----------------------------------+------------------------------------------------------------------------------------------------------+
   | Element                           | Description                                                                                          |
   +===================================+======================================================================================================+
   | Location                          | Path of the object after parts have been merged.                                                     |
   |                                   |                                                                                                      |
   |                                   | Type: string                                                                                         |
   +-----------------------------------+------------------------------------------------------------------------------------------------------+
   | Bucket                            | Bucket in which parts are merged.                                                                    |
   |                                   |                                                                                                      |
   |                                   | Type: string                                                                                         |
   +-----------------------------------+------------------------------------------------------------------------------------------------------+
   | Key                               | Indicates the key of the generated object.                                                           |
   |                                   |                                                                                                      |
   |                                   | Type: string                                                                                         |
   +-----------------------------------+------------------------------------------------------------------------------------------------------+
   | ETag                              | The result calculated based on the ETag of each part is the unique identifier of the object content. |
   |                                   |                                                                                                      |
   |                                   | Type: string                                                                                         |
   +-----------------------------------+------------------------------------------------------------------------------------------------------+

Error Responses
---------------

#. If no message body exists, OBS returns **400 Bad Request**.
#. If the message body format is incorrect, OBS returns **400 Bad Request**.
#. If the part information in the message body is not sorted by part sequence number, OBS returns **400 Bad Request** and the error code is **InvalidPartOrder**.
#. If the AK or signature is invalid, OBS returns **403 Forbidden** and the error code is **AccessDenied**.
#. If the requested bucket is not found, OBS returns **404 Not Found** and the error code is **NoSuchBucket**.
#. If the requested multipart upload does not exist, OBS returns **404 Not Found** and error code **NoSuchUpload**.
#. If the user is not the initiator of the task, OBS returns **403 Forbidden** and the error code is **AccessDenied**.
#. If the request part list contains a part that does not exist, OBS returns **400 Bad Request** and the error code is **InvalidPart**.
#. If the Etag of the part contained in the request part list is incorrect, OBS returns **400 Bad Request** and the error code is **InvalidPart**.
#. If the size of a part other than the last part is smaller than 100 KB, OBS returns **400 Bad Request**.
#. If the size of the object is greater than 48.8 TB after parts being merged, OBS returns status code **400 Bad Request**.

Other errors are included in :ref:`Table 2 <obs_04_0115__d0e843>`.

.. _obs_04_0102__section74706439232:

Sample Request
--------------

.. code-block:: text

   POST /object02?uploadId=00000163D46218698DF407362295674C HTTP/1.1
   User-Agent: curl/7.29.0
   Host: examplebucket.obs.region.example.com
   Accept: */*
   Date: WED, 01 Jul 2015 05:23:46 GMT
   Authorization: OBS H4IPJX0TQTHTHEBQQCEC:dOfK9iILcKxo58tRp3fWeDoYzKA=
   Content-Length: 422

   <?xml version="1.0" encoding="utf-8"?>
   <CompleteMultipartUpload>
     <Part>
       <PartNumber>1</PartNumber>
       <ETag>a54357aff0632cce46d942af68356b38</ETag>
     </Part>
     <Part>
       <PartNumber>2</PartNumber>
       <ETag>0c78aef83f66abc1fa1e8477f296d394</ETag>
     </Part>
     <Part>
       <PartNumber>3</PartNumber>
       <ETag>acbd18db4cc2f85cedef654fccc4a4d8</ETag>
     </Part>
   </CompleteMultipartUpload>

Sample Response
---------------

::

   HTTP/1.1 200 OK
   Server: OBS
   x-obs-request-id: 8DF400000163D4625BE3075019BD02B8
   x-obs-id-2: 32AAAQAAEAABAAAQAAEAABAAAQAAEAABCSN8D1AfQcIvyGBZ9+Ee+jU6zv1iYdO4
   Content-Type: application/xml
   Date: WED, 01 Jul 2015 05:23:46 GMT
   Content-Length: 326

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <CompleteMultipartUploadResult xmlns="http://obs.example.com/doc/2015-06-30/">
     <Location>/examplebucket/object02</Location>
     <Bucket>examplebucket</Bucket>
     <Key>object02</Key>
     <ETag>"03f814825e5a691489b947a2e120b2d3-3"</ETag>
   </CompleteMultipartUploadResult>
